---
layout: post
title: Get Flutter's offline support in Supabase
date: '2022-09-13T10:00:00.000-03:00'
author: Matías Irland
tags: [stock, supabase, flutter, firebase, firebase real-time database, dart, pub, package, plugin, stream, database, drift, realm, floor]
author_id: mirland
category: development
featured_image: /images/supabase-offline-suport/banner.png
permalink: /blog/get-flutter-offline-support-in-supabase/
---

[Supabase] is one of the most well-known open-source alternatives to [Firebase].
Although Supabase implements many Firebase features, one that I constantly crave is **offline support for the real-time database**. 

In this blog post, we’ll cover how you can use a local database as a [Supabase] cache through [Stock], a dart package that combines multiple data sources and gets one data `Stream`.
However, you can apply these concepts and ideas to diverse situations, such as adding offline support when using a Rest API.

To show how we can achieve that, we'll create a simple app that lists all of Xmartlabs' open-source projects, demonstrating how [Stock] helps us get excellent results.

# Architecture Overview

Although we want to build a simple app, we'll use the repository pattern, one of the most used patterns in Flutter nowadays.
If you don't know about it, I suggest checking out [this blog][repository_blog].

We will have two data sources, a remote and a local data source, which [Stock] will combine in the repository.

Because we want to use the real-time database, we'll use the [Supabase fluter package].
Although the package provides many features, you can use Supabase as a REST API.

Your local database will store this data.
In our case, we'll use [Floor] because it's simple and has many features.
If you'd prefer to use another one, there are a bunch of alternatives, such as [Drift] or [Realm], you can use.


<img width="100%" src="/images/supabase-offline-suport/arch_overview.png" />

We will use a `StatefulWidget` to display the data to simplify this Project. 
However, in an actual project, you should use a state management package, like [Bloc] or [Provider].

# Sample app: listing our company's OSS projects

As mentioned, we want to build an app that displays Xmartlabs' Open Source projects.

Here's how it will look:



<div style="text-align: center; margin-bottom: 15px;">
    <img  height="500px" width="auto" src="/images/supabase-offline-suport/sample_app.gif" />
</div>


First, we have to create a new Flutter project and the Project's entity.


```dart
class Project extends Equatable {
  final int id;
  final String name;
  final String description;
  final String url;
  final String imageUrl;
  final String language;

  // Ommited: Add constuctor, define props for equals and hashcode and add `fromJson` method
}
```

See the full implementation [here][ref_project_entity].

## Step 1: Remote Source - Supabase setup

Supabase setup is not complex, and there are [good tutorials][supabase_tutorial] showing how you can do this process.
In this case, I created a Supabase free project which contains only one table, `projects`.
This table is where the metadata for Xmartlabs' open-source projects will be stored.

<img width="100%" src="/images/supabase-offline-suport/supabase_table.png" />

Then I included the `supabase_flutter` package in the Flutter project.
I initialized the Supabase client and created the `ProjectSupabaseRemoteSource` with only one method that gets a `Stream` of projects using the Real Time Database.


```dart
  final client = await Supabase.initialize(
    url: Config.supabaseUrl,
    anonKey: Config.supabaseAnonKey,
  ).then((supabase) => supabase.client);
```

```dart
class ProjectSupabaseRemoteSource {
  final SupabaseClient _client;

  ProjectSupabaseRemoteSource(this._client);

  Stream<List<Project>> getRemoteProjectsStream() => _client
      .from('projects')
      .stream(['id'])
      .execute()
      .map((json) => json.map(Project.fromJson).toList());
}
```

You can see the full Supabase integration [in this commit][ref_supabase_implementation].

## Step 2: Local Source - Local Database setup

In this example, we'll use [Floor], a simple and powerful Data Base in Flutter.

Usually, we use separate entities for database and service, depending on your Project's complexity.
In this case, we'll use the same [Project][ref_project_entity] entity instead of different ones. 

After the setup, you will have two main classes:
- The `Project` entity will be mapped to a table.
- The DAO, which, in this case, will be our local source.
This class will have methods for getting and updating the database projects.

```dart
@Entity(tableName: 'projects')
class Project extends Equatable {
  @primaryKey
  final int id;
  // ... other fields
```

```dart
abstract class ProjectLocalSource {
  @Query('SELECT * FROM projects')
  Stream<List<Project>> getProjects();

  @Insert(onConflict: OnConflictStrategy.replace)
  Future<void> insertProjects(List<Project> projects);

  @Query('DELETE FROM projects')
  Future<void> deleteAllProjects();

  @transaction
  Future<void> replaceProjects(List<Project> projects) async {
    await deleteAllProjects();
    await insertProjects(projects);
  }
}
```

You can check the full database integration [here][ref_db_implementation].

## Step 3: Repository - Stock Integration

The previous steps were not difficult.
We created one entity and a couple of data sources.
However, this is the most exciting part, where we have to combine different data sources to get only one stream that contains the OSS projects.

**We will use [Stock]**, a dart package whose primary function is to combine these sources.
We need to provide stock two essential classes:
- `Fetcher`: a class to fetch the network data. Stock provides two types of fetchers.
  - `Stream`, ideal for this case, in which we use the Real Time Database.
  - `Future`, used, for example, if you are consuming a REST API.
- `SourceOfTruth`: a class that can store the fetched data in a local cache. In our case, the local cache is our [Floor] database.

Two types define these classes:
- The `Key`, a type commonly used to get de data. That key can have important information like an `id` or the current page number if you are fetching a list. In our example, we won't use it because we will bring all data just using one endpoint.
- The entity class, in our example a `List<Project>`. The `Fetcher` and the `SourceOfTruth` could use different types, but they should be mapped to the same type using a [StockTypeMapper].


```dart
class ProjectRepository {
  final Stock<dynamic, List<Project>> _stock;

  ProjectRepository(
    ProjectLocalSource projectLocalSource,
    ProjectSupabaseRemoteSource projectRemoteSource,
  ) : _stock = Stock<dynamic, List<Project>>(
          fetcher: Fetcher.ofStream(
            (_) => projectRemoteSource.getRemoteProjectsStream(),
          ),
          sourceOfTruth: SourceOfTruth<dynamic, List<Project>>(
            reader: (_) => projectLocalSource.getProjects(),
            writer: (_, projects) =>
                projectLocalSource.replaceProjects(projects ?? []),
          ),
        );

  Stream<StockResponse<List<Project>>> getProjects() => _stock.stream(null);
}
```

`Stock` provides a `Stream` of `StockResponse`, which has three possible values: `StockResponseLoading`, `StockResponseData`, or `StockResponseError`. 
With that `Stream`, we are ready to display the data and status in the UI.

Inspect the full implementation [in this commit][ref_stock_implementation].

## Step 4: Handle stock responses

In this last part, we'll handle the three different response types: the error, the data, and the loading state. 
To do that we will handle the responses in a `StatefulWidget`

The widget state will contain the list of projects and a bool that indicates if the data is loading or not.

```dart
class _OssProjectsPageState extends State<OssProjectsPage> {
  late StreamSubscription _subscription;

  List<Project>? projects;
  bool isLoading = false;

  @override
  void initState() {
    super.initState();
    _subscription = projectRepository.getProjects().listen((response) {
      if (response.isData) {
        setState(() {
          projects = response.requireData();
          if (isLoading && response.origin == ResponseOrigin.fetcher) {
            isLoading = false;
          }
        });
      } else if (response.isLoading) {
        setState(() => isLoading = true);
      } else {
        if (isLoading && response.origin == ResponseOrigin.fetcher) {
          setState(() => isLoading = false);
        }
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(
          content: Text(
            'An error happened!: ${(response as StockResponseError).error}',
          ),
        ));
      }
    });
  }

  @override
  void dispose() {
    _subscription.cancel();
    super.dispose();
  }
}
```

So the last thing is using the state to display the data:

```dart
class _OssProjectsPageState extends State<OssProjectsPage> {
  //.... previous code
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Xmartlabs OSS Projects')),
      body: Stack(
        alignment: AlignmentDirectional.center,
        children: [
          ListView.builder(
            padding: const EdgeInsets.all(8.0),
            itemCount: projects?.length ?? 0,
            itemBuilder: (context, index) =>
                _ProjectWidget(project: projects![index]),
          ),
          if (isLoading) const CircularProgressIndicator(),
        ],
      ),
    );
  }
}
```

And this is the end result!

<div style="text-align: center; margin-bottom: 15px;">
    <img height="500px" width="auto" src="/images/supabase-offline-suport/final_sample_app.gif" />
</div>

As you can see, the OSS projects are displayed fast, and there's no difference between online and offline.


The complete example is on [GitHub](https://github.com/mirland/supabase-offline-support-with-stock/), so go ahead and check it out!

# Conclusion

This blog analyzed how we can integrate offline support easily to Supabase.
Furthermore, if we replace [Supababse] with another provider or simply use a rest API, the code will be the same. 
So if your data layer changes, you don't have to make any changes to your presentation layer, which is one of the essential aspects of this architecture.

In my experience, offline support moves app experience to the next level.
You can remove ugly spinners and give feedback to the user instantaneously. So making an effort to achieve it is worth it. 

We also had a glimpse of how [Stock] helped us to achieve this feature.
The package did the most challenging tasks, such as synchronizations, state reporting, and data storing, allowing the app to run extremely fast.

I encourage you to try it out and share your feedback and contributions!

[Bloc]: https://pub.dev/packages/bloc
[Drift]: https://pub.dev/packages/drift
[Firebase]: https://firebase.google.com/
[Floor]: https://pub.dev/packages/floor
[GetIt]: https://pub.dev/packages/get_it
[Provider]: https://pub.dev/packages/provider
[Realm]: https://pub.dev/packages/realm
[ref_db_implementation]: https://github.com/mirland/supabase-offline-support-with-stock/commit/b46cb20f22453448718b85fcd63b811ad51afd11
[ref_stock_implementation]: https://github.com/mirland/supabase-offline-support-with-stock/commit/0492f2d257e93333bd343e303cd597eb9d80554a#diff-f3374e5f8e848d41b528d205b7a44d6d2642049a5f7a5c78d51b74f0116596f2R6
[ref_project_entity]: https://github.com/mirland/supabase-offline-support-with-stock/commit/baccd9463d6703cb10df69e6cb13e21950e028f6#diff-fc21a29884a4f9313eb6bd5bc24aad30604d0de4d096488d739035aa2356850aR3
[ref_supabase_implementation]: https://github.com/mirland/supabase-offline-support-with-stock/commit/f4fcea6036e82dbfa4b53afd28378ed63098f1d4
[repository_blog]: https://davidserrano.io/data-layer-in-flutter-use-the-repository-pattern-to-keep-a-local-copy-of-your-api-data
[Stock]: https://pub.dev/packages/stock
[StockTypeMapper]: https://pub.dev/packages/stock#use-different-types-for-fetcher-and-sourceoftruth
[Supabase fluter package]: https://pub.dev/packages/supabase_flutter
[supabase_tutorial]: https://supabase.com/docs/guides/with-flutter
[Supabase]: https://supabase.com/
