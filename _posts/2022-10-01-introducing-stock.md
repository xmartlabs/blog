---
layout: post
title: Introducing stock
date: '2022-09-01T10:00:00.000-03:00'
author: Matías Irland
tags: [stock, flutter, dart, pub, package, plugin, hacktoberfest]
author_id: mirland
category: development
featured_image: /images/supabase-offline-suport/banner.png
permalink: /blog/introducing-stock/
---


October is an important month for Open Source contributors because [Hacktoberfest] is celebrated.
In this wonderful month, we are extremely happy to announce [**Stock**][stock], the latest Xmartlabs' Flutter Open Source Project.

## What is [Stock]? 

[Stock] is a dart package whose main feature is combining different data sources on Flutter.
Most mobile projects need the same thing, share data with a cloud service. 
For instance, it could be a Rest API or a real-time service like [Firebase Database][firebase_rtd] or [Supabase].
If it's your case, this blog may be useful for you.

Stock is based on the repository pattern, one of the most used patterns in mobile.
A repository uses different data sources, we usually use a remote and a local data source.
[Stock] was created to make this process smooth, it allows you to combine these data sources and get one data `Stream` containing its states.
Furthermore, if you only use a remote source, Stock can be used as a local cache, so in a few lines of code, you can improve your app experience.

[IMAGEN ISA]

## Should I consider caching the network data? 

[Stock] exists because of the need of adding a cache. It could be a memory or disk cache, but that's the point here.
Should I need a cache in my app?

From my point of view, it's an excellent question that should be done.
Nowadays in most places, the internet connection is good, and phone resources are better than before, so why should I waste time adding a local cache?

And the answer is simple, you are not wasting time, we are saving time.
The cache allows you to leverage the app experience, removing ugly loading indicators, adding better transitions, and at the end, making your user happier.

On the other hand, having a stream that emits the data changes helps us to make our code better, avoid issues and have consistency in our app.

Some services like Supabase, provide a data stream.
However, if we use just a remote service, like a Rest API, creating this stream could not be straightforward.
We can do it, but it could be a headache.
Using Stock, get a data stream is trivial, so this is why we should consider adding [Sock] in our project.


## How does it work?

Stock uses two important components:
- The `Fetcher` defines how data will be fetched over the network.
- The `SourceOfTruth` defines how local data will be read and written in your local cache. Although Stock can be used without it, its use is recommended.

Suppose that we have an app which displays the Tweets of a particular user.
In this case, we can create our `Fetcher` and `SourceOfThruth` in this way:

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

Now we have done the hardest work, but how should I use it?
Stock provides some methods to get the data, but the most important one is `steam()`. 
It returns a `Stream` of data containing the data state. 

This state has 3 possible values:
- Data: New data arrived 
- Error: Something went wrong
- Loading: The data is loading

```dart
  stock
      .stream(userId, refresh: true)
      .listen((StockResponse<List<Tweet>> stockResponse) {
    if (stockResponse is StockResponseLoading) {
      _displayLoadingIndicator();
    } else if (stockResponse is StockResponseData) {
      _displayTweetsInUI((stockResponse is StockResponseData).data);
    } else {
      _displayErrorInUi((stockResponse as StockResponseError).error);
    }
  });
```

## What's next?

In this blog, we analyzed why it's important adding a cache layer, we gave a brief introduction to Stock and its main features.
However, if you want to go further, I recommend you to read the [project documentation][stock] and try it out.

We have been using this plugin internally with excellent results and now we are announcing the first stable release!
One of the greatest things of this plugin is that it's flexible and it could be used in multiple situations.
An interesting example is how [it can be used to add offline support in Supabase][suppabase_blog].

All feedback is welcome and if you liked it don't forget to [give us a star][stock_gh]!


[Hacktoberfest]: https://hacktoberfest.com/
[stock]: https://pub.dev/packages/stock
[stock_gh]: https://github.com/xmartlabs/stock
[firebase_rtd]: https://firebase.google.com/docs/database
[supabase]: https://supabase.com/
[suppabase_blog]: https://lxmartlabs.com/blog/get-flutter-offline-support-in-supabase/
