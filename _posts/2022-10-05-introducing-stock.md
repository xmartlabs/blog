---
layout: post
title: Introducing stock
date: '2022-10-05T09:00:00.000-03:00'
author: Matías Irland
tags: [stock, flutter, dart, pub, package, plugin, hacktoberfest]
author_id: mirland
category: [mobile-development]
featured_image: /images/introducing-stock/banner.png
permalink: /blog/introducing-stock/
---


October is a special month for Open Source contributors thanks to [Hacktoberfest] taking place.
In this wonderful month, we are thrilled to announce [**Stock**][stock], Xmartlabs' latest Flutter Open Source Project.

## What is [Stock]?

[Stock] is a dart package whose main feature is combining different data sources on Flutter.
Most mobile projects need the same thing, to share data with a cloud service.
For instance, it could be a Rest API or a real-time service like [Firebase Database][firebase_rtd] or [Supabase].
If this is your case, this blog may be helpful for you.

Stock is based on the repository pattern, one of the most used patterns in mobile.
A repository uses different data sources, we usually use a remote and a local data source.
We created [Stock] to make this process smoother. It allows you to combine these data sources and get one data `Stream` containing its states.
Furthermore, if you only use a remote source, Stock can be used as a local cache, improving your app experience in just a few lines of code.

<img width="100%" src="/images/introducing-stock/repository-pattern.jpg" />


## Should I consider caching the network data?

[Stock] exists because of the need to add a cache. It could be a memory or disk cache, but it doesn't really matter which type are you using, instead it only matters the need of one.
You may ask, do I need a cache in my app?

From my perspective, that's an excellent question, and one that should be asked.
Nowadays, the internet connection is good in most places, and phone resources have never been better, so why waste my time adding a local cache?

The answer is simple: you are not wasting time, you are saving it.
The cache allows you to leverage the app experience, removing ugly loading indicators, adding better transitions, and, in the end, making your user happier.

On the other hand, having a stream that emits the data changes helps us improve our code, avoid issues, and have consistency in our app.

Some services, like Supabase, provide a data stream.
However, creating this stream might not be that straightforward if we use a remote service, like a Rest API.
We can do it, but it could become a headache.
With [Stock], getting a data stream is trivial, that's why you should consider adding it to your project.


## How does it work?

Stock uses two important components:
- The `Fetcher` defines how data will be fetched over the network.
- The `SourceOfTruth` defines how local data will be read and written in your local cache. Although Stock can be used without it, we recommend its usage.

Suppose that we have an app that displays the Tweets of a particular user.
In this case, we can create our `Fetcher` and `SourceOfThruth` in the following way:

```dart
  final fetcher = Fetcher.ofFuture<String, List<Tweet>>(
    (userId) => _api.getUserTweets(userId),
  );

  final sourceOfTruth = SourceOfTruth<String, List<Tweet>>(
    reader: (userId) => _database.getUserTweets(userId),
    writer: (userId, tweets) => _database.writeUserTweets(userId, tweets),
  );

```

Then we can proceed to create the `Stock`, which will be used in the repository:

```dart
  final stock = Stock<String, List<Tweet>>(
    fetcher: fetcher,
    sourceOfTruth: sourceOfTruth,
  );
```

Now that we've done the hardest work, how should you use it?
Stock provides some methods to get the data, but the most important one is `stream()`.
It returns a `Stream` of data containing the data state.

This state has 3 possible values:
- Data: New data arrived
- Error: Something went wrong
- Loading: The data is loading

```dart
  stock
      .stream(userId, refresh: true)
      .listen((StockResponse<List<Tweet>> stockResponse) {
        stockResponse.when(
          onLoading: (origin) => _displayLoadingIndicator(),
          onData: (origin, data) => _displayTweetsInUI(data),
          onError: (origin, error, stacktrace) => _displayErrorInUi(error),
        );
      });
```

## What's next?

In this blog, we analyzed why adding a cache layer is essential, and we gave a brief introduction to Stock and its main features.
However, if you want to go further, I recommend you read the [project documentation][stock] and try it out.

We have been using this plugin internally with excellent results and now we are announcing the first stable release!
One of the greatest things about this plugin is its flexibility to be used in multiple situations.
An interesting example is [using it to add offline support in Supabase][suppabase_blog].

So go check it out, we welcome any feedback you have. If you like it, don't forget to [give us a star][stock_gh]!


[Hacktoberfest]: https://hacktoberfest.com/
[stock]: https://pub.dev/packages/stock
[stock_gh]: https://github.com/xmartlabs/stock
[firebase_rtd]: https://firebase.google.com/docs/database
[supabase]: https://supabase.com/
[suppabase_blog]: https://blog.xmartlabs.com/blog/get-flutter-offline-support-in-supabase/
