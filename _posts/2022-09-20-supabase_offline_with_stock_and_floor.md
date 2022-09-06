---
layout: post
title: Flutter Supabase offline support with Stock
date: '2022-08-19T10:00:00.000-03:00'
author: Matías Irland
tags: [stock, supabase, fluter, firebase, firebase real-time database]
author_id: mirland
category: development
featured_image: /images/image-completion/image-completion.png
permalink: /blog/supabase-offline-support-with-stock/
---

[Supabase] is one of the most well-known open-source [Firebase] alternatives.
Although a lot of Firebase features are implemented by it, there's one that I miss a lot, **the offline support for the real-time database**.

In this post, we will cover how can we can use a local database for catching [Supabase] data using [Stock], a dart package used to combine multiple data sources and get one data `Stream`.
However, these concepts and ideas can be applied to multiple/different situations, such as adding offline support when you are using a Rest API.

To show how we can achieve that, in this blog post we will create a simple app, which lists all open-source Xmartlabs' projects, showing how [Stock] helps us to get excellent results.

# Arch Overview

Despite we want to build a simple app, we'll use the repository pattern, one of the most used patterns in Flutter nowadays.
If you don't know it, I recommend you check [this blog][repository_blog].

We will have 2 data sources, a remote and a local data source that will be combined by [Stock] in the repository.

As we want to use the real-time database, we'll use the [Supabase fluter package].
Although the package provides a lot of features, Supabase also can be used as a REST API.

This data will be cached in a local database, in our case, we'll use [Floor] because it's simple and it has a lot of features. If you prefer to use another one, there are a bunch of alternatives such as [Drift] or [Realm] that you can use.


METER IMAGEN DE COMO QUEDA LA

To make this project simpler, we will use just a `StatefulWidget` to display the data.
However, in a real project, you should use a state management package, like [Bloc] or [Provider].

# Build Xmartlabs OSS Project sample app

As we mentioned, we want to build an app to display some of Xmartlabs' Open Source projects.

Here is how it will look:


ADD GIF

At the beginning, we have to create a new Flutter project and create the Project entity.


```dart
class Project extends Equatable {
  final int id;
  final String name;
  final String description;
  final String url;
  final String imageUrl;
  final String language;

  // TODO: Add constuctor, define props for equals and hascode and add `fromJson` method
}
```

Full implementation [here][ref_project_entity].

## Remote Source - Supabase setup

Subabase setup is not hard, it has [good tutorials][supabase_tutorial] which shows how you can do this process. 
In our case, I created a Supabase free project which contains only one table, `projects`.
This table is used to store the open-source Xmartlabs' project metadata.

AGREGAR IMAGEN DE LA TABLA

Then I included the `supabase_flutter` package in the flutter project, I initialized the Supabase client and I created the `ProjectSupabaseRemoteSource` with only one method, a method to get a `Stream` of projects using the Real Time Database.


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

The full Supabase integration could be seen [in this commit][ref_supabase_implementation].

## Local Source - Local Database setup

On Flutter, we have a bunch of database alternatives, in this app we will use [Floor].

An important comment is in this case we will use the same [Project][ref_project_entity] entity instead use different entities for database and service.
We usually use different entities, but it depends on your project's complexity.

After the setup, you will have two important classes:
- The `Project` entity will be mapped to a table.
- The DAO, which in this case will be our local source. This class will have methods for getting and updating the database projects.

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

## Repository - Stock Integration

The previous steps were not hard, we have created one entity and a couple of data sources.
However, now is the most interesting part, the part where we have to combine different data sources to get only one stream, a stream that contains the OSS projects.

To combine these sources **we will use [Stock]**, a dart package that is its main function.
We need to provide stock two important classes:
- A `Fetcher`, a class to fetch the network data.
Stock provides two types of fetchers: a fetcher from a `Stream` (ideal for this case that we are using the Real Time Database) or from a `Future` (used for example if you are consuming a REST API). 
- A `SourceOfTruth`, a class that can store the fetched data in a local cache, in our case the local cache is our [Floor] database.

These classes are defined by two types:
- The `Key`, a type used to get de data. That key can have important information like an `id`, or the current page number if you are fetching a list.
In our example. we will not use it because we will fetch all data just using one endpoint.
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

`Stock` provides a `Stream` of `StockResponse`, which has 3 possible values: `StockResponseLoading`, `StockResponseData` or `StockResponseError`. 
With that `Stream` we are ready to display the data and the state in the UI.

The full implementation could be checked [in this commit][ref_stock_implementation].

### Handle stock responses

This is the last part, where we handle the 3 different response types, the error, the data and the loading state.
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

You can check the full example on [GitHub](https://github.com/mirland/supabase-offline-support-with-stock/).

# Conclusion

In this blog, we analyzed how we can integrate offline support easily to Supabase.
Furthermore, if we replace [Supababse] with another provider, or use just a rest API the code will be the same.
So that is one of the most important things about this architecture, the Data layer could change, and you don't have to do any changes to your presentation layer.

In my experience, offline support moves the app experience to the next level.
You can remove ugly spinners, and give feedback to the user instantaneously.

On the other hand, we saw how [Stock] helped us to achieve this feature.
The hardest work such as synchronizations, state reporting, store the data, was done by the package, so it allows app to move very fast.

I invite you to try it and do not forget to share your feedback!

[Bloc]: https://pub.dev/packages/bloc
[Drift]: https://pub.dev/packages/drift
[Firebase]: https://firebase.google.com/
[Floor]: https://pub.dev/packages/floor
[GetIt]: https://pub.dev/packages/get_it
[Provider]: https://pub.dev/packages/provider
[Realm]: https://pub.dev/packages/realm
[ref_db_implementation]: https://github.com/mirland/supabase-offline-support-with-stock/commit/b46cb20f22453448718b85fcd63b811ad51afd11
[ref_stock_implementation]: hhttps://github.com/mirland/supabase-offline-support-with-stock/commit/0492f2d257e93333bd343e303cd597eb9d80554a#diff-f3374e5f8e848d41b528d205b7a44d6d2642049a5f7a5c78d51b74f0116596f2R6
[ref_project_entity]: https://github.com/mirland/supabase-offline-support-with-stock/commit/baccd9463d6703cb10df69e6cb13e21950e028f6#diff-fc21a29884a4f9313eb6bd5bc24aad30604d0de4d096488d739035aa2356850aR3
[ref_supabase_implementation]: https://github.com/mirland/supabase-offline-support-with-stock/commit/f4fcea6036e82dbfa4b53afd28378ed63098f1d4
[repository_blog]: https://davidserrano.io/data-layer-in-flutter-use-the-repository-pattern-to-keep-a-local-copy-of-your-api-data
[Stock]: https://pub.dev/packages/stock
[StockTypeMapper]: https://pub.dev/packages/stock#use-different-types-for-fetcher-and-sourceoftruth
[Supabase fluter package]: https://pub.dev/packages/supabase_flutter
[supabase_tutorial]: https://supabase.com/docs/guides/with-flutter
[Supabase]: https://supabase.com/
