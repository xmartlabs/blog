---
title: 'A bright future ahead: React Native in App.js Conf 2022'
layout: post
permalink: /a-bright-future-ahead-react-native-appjs-conf/
date: '2022-06-23T10:00:00:000-03:00'
category: [mobile-development, development]
tags:
  - Mobile
  - Cross-Platform
  - React Native
author_id: nicoh
author: Nicolas Hernandez

featured_image: /images/rn-future/app.js-takeaways-react-native.png
---

## **Introduction**

Last week was the App.js Conf 2022

It has been almost two years since the App.js Conf 2020 was canceled due to the global pandemic. This year it came back as a hybrid event that allowed all developers around the world to attend the in-person talks online.

It was two days full of talks, workshops, and news regarding React Native’s present and future. In this post, we’ll discuss some of the most important things we believe are gonna generate impact in the ecosystem ( we are not planning to cover all the conf if you want that you can check this link here).

## **The new architecture is here to stay**

RN 68.X is the current version, and it comes with the possibility to enable Fabric and some tools from the new architecture. All of this is here to achieve more sophisticated solutions through the creation of better apps, with improved performance and tools.

Obviously, it’s gonna take some time for the community to progressively adopt it in all the third parties and provide support, but we are in a good place.

The current timeline presented by @cortinico in his talk displays the future of the architecture with the upcoming versions of React Native.

![timeline](/images/rn-future/rn-timeline.png)

Another important aspect regarding the new architecture discussion and when to adopt it is discussed in the next slide.

![react-next-versions](/images/rn-future/react-next-versions.png)

As we can see in the image, as soon as we reach RN 69.X things are gonna be different. For the first time, the new and the old architecture are gonna have different tools for us developers.
Even with RN 69.X, the old architecture is gonna support React 18 in some kind of legacy mode instead of supporting it fully. The new architecture, on the other hand, is gonna have full support for React 18 and all his new toolset for things like a concurrent mode (such as startTransition), new hooks, and lots of tools that could improve our solutions.

That's a really good argument in favor of moving towards the new architecture in upcoming projects.

## **Expo**

Expo has improved greatly since the last time, with its addition of EAS (read about it if you don't know what it is 🙏🏻), and a crazy amount of new features and cool stuff to improve the development time and also make the experience a lot smoother for React Native developers.

In this session, they made a lot of announcements along this line, some of them being game-changers to the experience of developing with Expo.

### EAS Metadata

This feature adds a new `store.config.json` file in your Expo app and it will ultimately enable you to automate the entire submission process for your app, filling in some information for the App Store very easily. For example in the picture below we can see this file and what the metadata and screenshots look like, all of this will be handled by Expo for you via EAS Metadata.

![EAS-metadata](/images/rn-future/EAS-metadata.jpeg)

Another cool feature about EAS Metadata is that it will be able to be instantly linted against the most common known issues to warn you about any potential App Store rejection, saving you time for in-app submission process.

![EAS-metadata-lint](/images/rn-future/EAS-metadata-lint.gif)

Also, EAS Metadata can be automated to perform actions like localizing and deploying to every App Store around the world.

[EAS-distribution](/images/rn-future/EAS-distribution.gif)

### Expo Cli

In the next version of Expo SDK 46 they will be moving to a new versioned CLI `npx expo`. It’s more stable, more flexible, and simplifies CI usage (caching, versioning, etc.). This aims to replace the actual 'expo-cli' in the future.

Also `Eject` has been replaced by `Prebuild` in the new CLI mentioned above. All Expo apps can use any native code via Config Plugins, you can make your own Config plugins to add functionality. The reasons eject from Expo are becoming even less.

![new-expo-cli.jpeg](/images/rn-future/new-expo-cli.jpeg)

The new `npx expo` will also be getting React Suspense in development mode. This allows deferring bundling components until they are mounted (some kind of lazy loading), making larger apps with a lot of components to bundle very quickly.

![lazy-bundling.jpeg](/images/rn-future/lazy-bundling.jpeg)

`Create Expo App` is the official replacement for the command "expo init". With the new versioned CLI coming to SDK 46, you'll no longer need to install Expo CLI to get started with Expo.

![create-expo-app.gif](/images/rn-future/create-expo-app.gif)

## **FlashList**

During the past years, Shopify has been sponsoring and investing a lot of coal in the React Native community. One example of this is the well-known `react-native-skia` .

As a vetted React Native developer, one of the most frustrating aspects of developing in React Native is achieving a fast scrolling list, with good performance and good customization.

First, we have the ListView that was deprecated long ago, and now we have FlatList, it improves a lot if we compare it with its ancestor but it still has some performance issues if the components are a bit heavy or if you have a lot of them (you could avoid mostly 99% of the issues with some performance optimization).

I know there are some packages with recycling and some cool stuff but all of them have trouble and don’t work that well compared to the FlatList.

![flashlist.gif](/images/rn-future/flashlist.gif)

This announcement of Flashlist promises to be a drop-in of FlatList being built on top of a RecyclerListView and aims to have pretty good performance even in low-end devices. That's all good news for us taking into account Shopify’s reputation and the problem they want to tackle.

It’s gonna be available for everyone soon, so keep a lookout for it ⚡

## **REASSURE**

Callstack is known as one of the most important companies in React Native, along with Software Mansion and others. They also contribute a lot to OSS and have amazing libraries like `react-native-paper` , `react-native-builder-bob`, and many more.

Now they are cooking something to simplify and make performance monitoring in a React/React Native app easier. They call this Reassure (it's in open beta now but it will available soon).

They don’t want to attack a common bug but one of the most troublesome ones in React Native, performance bugs, better known as `performance regression`. They mentioned the performance will fall apart eventually if unattended, but we don't know **when.**

That’s the main purpose of Reassure, plus together with some kind of testing, it’ll help us catch this regression when we add new code. There are some other tools in the market to monitor performance but none of them do what Reassure tries to.

Another good thing about this kind of test is that they make a huge impact. It’s not like we’re aiming to test everything and achieve 100% coverage but we test what matters most, 80% of the time developers are solving issues whose origin is the JS thread.

So, let’s see how this works.

It’s based in our common testing libraries, it’s pretty simple to write a test (as you can see below), and it’s pretty simple to refactor our current existing tests.

```tsx
test('Count increments on press', async () => {
  const scenario = async (screen: RenderAPI) => {
    const button = screen.getByText('Action');

    await screen.findByText('Count: 0’);
    fireEvent.press(button);
    fireEvent.press(button);
    await screen.findByText('Count: 2');
  };

  const stats = await measureRender(
    <Counter />,
    { scenario, runs: 20 }
  );
  await writeTestStats(stats);
});
```

It runs your test once for your current branch and then runs it again against your main branch, later it compares the results to provide meaningful information. In the future this may change, getting all the work done just by running once.

![reassure-test](/images/rn-future/reassure-test.png)

As you can see, it's pretty simple to use and the report it’s very neat and useful. It could also be run in any CI that you want.

![reassure-ci](/images/rn-future/reassure-ci.png)

## **Final thoughts**

As I said in the beginning, these do not cover the whole event by any standard. However, they are improvements and tools that will definitely change the way we use React Native. It’s important to keep a watchful eye on some of these releases because they will more likely affect your work on future projects.

Overall, App.js Conf it’s a truly enriching event, not only to keep an eye on specific technologies, and tools but also to take the pulse of the market and the projects that are currently rocking it. I’d highly recommend giving it a go next year if you have the chance.
