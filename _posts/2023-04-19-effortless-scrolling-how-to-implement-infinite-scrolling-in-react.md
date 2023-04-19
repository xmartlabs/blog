---
layout: post
title: Mastering Infinite Scrolling with React Native
date: '2023-04-19T09:00:00.000-03:00'
tags: [React Native]
author_id: solo
category: [development, web-development]
permalink: /blog/how-to-implement-infinite-scrolling-in-react-native/
featured_image: /images/effortless-scrolling/Infinite_scrolling.png
---

![Infinite scrolling.png](/images/effortless-scrolling/Infinite_scrolling.png)

## Introduction

In today's world of mobile apps, user experience is everything. And when it comes to delivering a seamless and engaging experience, infinite scrolling can be a game-changer. Whether it's browsing through social media feeds, product lists, or news websites, infinite scrolling can make it easier for users to consume more content without having to click through pages.

If you're looking for a way to improve the user experience of your React Native app, implementing infinite scrolling doesn't have to be a complex process. In fact, we've found a simple and fast solution that can make all the difference in creating an app with a smooth UX. In this blog, we'll show you how to implement infinite scrolling using FlatList in your React Native app, and why it's worth considering for your next project.

## What is Infinite Scrolling

Infinite scrolling is a popular design technique used in modern websites and mobile applications that enhances the user experience by allowing content to load automatically as the user scrolls down the page or screen. This means that there's no need for the user to click or tap on a "next page" button to access more content. Instead, the new content is dynamically loaded in the background as the user reaches the end of the current content.

One of the main advantages of infinite scrolling is that it provides the user with a seamless and uninterrupted browsing experience. This means that users can browse through a large amount of content without having to manually navigate between pages or screens, resulting in a more engaging and efficient browsing experience.

Infinite scrolling has become a universal design pattern in various digital platforms and industries. Major social media apps such as TikTok, Instagram, and Twitter have implemented infinite scrolling to deliver a seamless and uninterrupted browsing experience. News websites like CNN and the BBC have also incorporated infinite scrolling to allow readers to easily navigate through a large amount of content. Additionally, e-commerce giants like Amazon and eBay use this design technique to allow users to browse through a vast number of products without interruption.

![Comp-7.gif](/images/effortless-scrolling/Comp-7.gif)

## How Infinite Scrolling Works

Nowadays it is not rare at all that given a set of use cases within an app, a scrollable list containing a large number of elements is required.

In most case scenarios the elements that make up the list (the products, publications, news articles, etc.) come from a REST API, in which the endpoints in charge of providing them normally use pagination.

Implementing a scrollable list with pagination might get tedious, and sometimes it does. But it turns out that some time ago a discovered a very simple way to do so in **React Native** by using a third-party library.

## How to Implement Infinite Scrolling

### 1. Choose a component

First of all, we'll need a component to be able to implement a list. I could use something fancy like [FlashList](https://shopify.github.io/flash-list/) or [RecyclerListView](https://github.com/Flipkart/recyclerlistview). Still, in this post, I'll go for the [FlatList](https://reactnative.dev/docs/flatlist), simply because it comes within the core of RN, it offers us everything we need, and in case someone wants to opt for another, its Migration should be something trivial. Let's not lose sight of the fact that this post's focus is not to compare lists or talk about performance, but to expose a simple way to implement lists with infinite scrolling.

### 2. Trigger the action to load new items

Now that we have chosen our component, let's move on. What we need is a way to trigger an action to load new items into the list property once the user scrolls to the end. To do this, the `FlatList` has an `onEndReached` callback that allows us to provide a function to ask for new pages.

```jsx
<FlatList
  data={myList}
  renderItem={renderItem}
  keyExtractor={(item) => item.id.toString()}
  onEndReached={fetchNextPage}
  extraData={albums}
/>
```

Nothing out of this world, right? All we have pending now is how to load that list, ask for new pages and perform some type of caching.

### 3. Fetch the lists and cache the data

For this, we will use a third-party library [react-query](https://react-query-v3.tanstack.com/). It is a library for managing server state in React applications. It provides a powerful and flexible approach to data fetching and caching, which can greatly simplify the code required to manage asynchronous data in React applications.

I honestly don't remember if the authors mention it but I have the feeling that their API is inspired by `GraphQL` since it makes a distinction between two types of basic operations that are typical of the standard, `queries`, and `mutations`. A `query` refers to those operations that are limited to only querying entity data coming from a REST API while `mutation` refers to those operations that could eventually mutate it.

It is very important to make this clarification since both will manipulate the cache of the data processed from the responses to the API in very different ways.

The [useQuery](https://react-query-v3.tanstack.com/reference/useQuery#_top) hook is commonly used to wrap those calls to the server in which data is consulted, but for our specific case, we will be interested in using [useInfiniteQuery](https://react-query-v3.tanstack.com/reference/useInfiniteQuery#_top). I won't go into detail explaining how the [useQuery](https://react-query-v3.tanstack.com/reference/useQuery#_top) hook works, but I encourage you  to consult the documentation if it's something you're interested in.

With this hook, our problem will be as simple as declaring an asynchronous function that will be mainly in charge of making the call to our server and return in response the parsed data in proper conditions to be persisted in the entity's cache. Minimally the function should receive as a parameter the page index.

As a practical example, I will use a server that is exposing an endpoint to ask for photo albums. Let's focus on the way we make requests with paging and not on the nature of the server and endpoints.

```jsx
const PAGE_SIZE = 10;

const fetchAlbums = async (page: number): Promise<Album[]> => {
  const params: RawParams = {
    page_num: page,
    page_size: PAGE_SIZE,
  };

  const res = await axios.get<ServerAlbums>(Endpoints.GetAlbums, {
    params,
  });
  const rawAlbums = res.data;

  const albums: Album[] = rawAlbums.data.map((albumRaw) => {
    const album: Album = {
      clientName: albumRaw.title,
      coverUrl: albumRaw?.cover_thumbnail_url,
      id: albumRaw.id,
      updatedAt: DateTime.fromISO(albumRaw.last_update),
    };

    return album;
  });

  return albums;
};
```

We will wrap that asynchronous function using the `useInfiniteQuery` hook.

```jsx
export const useAlbumsQuery = (params: Params) => {
  const res = useInfiniteQuery(
    [QueryKeys.Albums, params],
    ({ pageParam = 1 }) => fetchAlbums(pageParam),
    {
      onError: (error) => {
        if (error.response.status !== 424) {
          logError(strings.networkingError);
        }
      },
      getNextPageParam: (lastPage, allPages) => {
        return allPages.length + 1;
      },
      keepPreviousData: true,
    }
  );

  const albumPages = res.data?.pages ?? [];
  const albums = flatten(albumPages);

  return { ...res, data: albums };
};
```

Note that if we are in a scenario in which we want to concatenate the new page to the previous ones, it is necessary to set the `keepPreviousData` flag to true.

Now that we have our hook, integrating it into our `FlatList` is very easy.

```jsx
const MyList = () => {
  const { data, fetchNextPage } = useAlbumsQuery();

  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      keyExtractor={(item) => item.id.toString()}
      onEndReached={fetchNextPage}
      extraData={albums}
    />
  );
};
```

### Conclusion

Ensuring cache integrity is typically one of the most challenging tasks in software development, and the use of the `react-query` library greatly facilitates it.

Using `react-query` with list components to implement an infinite scrolling list provides several benefits:

- It simplifies the process of fetching and caching data from an API.
- React-Query automatically handles data fetching and cache management, allowing developers to focus on implementing the UI.
- React-Query provides advanced features such as caching, stale-while-revalidate, and automatic refetching.
- It allows for a performant and efficient rendering of the list, even when dealing with large datasets.

As an engineer, I believe we should always aim to pursue the simplest solutions. The implication of something being simple is that the less complex something is, the less it will break, and the easier it is to maintain.

<aside>
👉 Looking to improve your React Native app's user experience? Our development team specializes in creating products that delight users and implementing solutions quickly and efficiently. Whether it's implementing infinite scrolling or any other feature that makes your app more intuitive and enjoyable to use, we've got you covered. Let's work together to take your app to the next level. <a data-mode="popup" class="typeform-share" href="https://form.typeform.com/to/c7G2RUWm">Contact us</a> today to learn more!
</aside>