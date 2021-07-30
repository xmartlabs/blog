---
layout: post
title: Introducing PagerTabStrip! - Finally a PagerView in pure SwiftUI
date: '2021-08-02T10:00:00.000-03:00'
author: Martin Barreto
tags: [Xmartlabs, PagerTabStrip, SwiftUI, XLPagertabStrip]
author_id: mtnBarreto
show: true
category: development
featured_image: /images/extending-material-theme-in-jetpack-compose/banner.jpeg
social_image: /images/extending-material-theme-in-jetpack-compose/banner_social.jpeg
twitter_image: /images/extending-material-theme-in-jetpack-compose/banner_twitter.jpeg
permalink: /blog/:title/
---

We're incredibly thrilled to announce PagerTabStrip, the most powerful pager view fully written in SwiftUI.

Creating a production-ready pager view could take several hours, even days of an engineering team. Such is the demand for pager views that Apple introduced a pager version on top of its native TabView recently but it lacks flexibility, its customization level is so limited that ends up not working in most cases.

What if I told you that with the PagerTabStrip you can create those pagers in a matter of minutes and not days. This exactly was our vision when we started to build this flexible yet powerful library.

Let's move on and see how you can build a sophisticated pager view in terms of seconds, a code snippet worth more than a thousand words 😂.

<img align="right" width="30%" src="/images/pager-swiftui/LogOutExample.gif"/>

```swift
struct MyPagerView: View {
	...
	..
	.
	var body: some View {
        PagerTabStripView() {
            MyHomeView(model: $homeModel).pagerTabItem {
                MyNavBarItem(title: "Home", imageName: "home")
            }.onPageAppear {
                homeModel.reloadData()
            }

            MyTrendingView(model: $trendingModel).pagerTabItem {
                MyNavBarItem(title: "Trending", imageName: "trending")
            }
            .onPageAppear {
                trendingModel.reloadData()
            }
            if user.isLoggedIn {
                MyProfileView().pagerTabItem {
                    MyNavBarItem(title: "Account", imageName: "account")
                }
            }
        }
        .pagerTabStripViewStyle(PagerTabViewStyle(tabItemSpacing: 0, 
                                                  tabItemHeight: 70, 
                                                  indicatorBarHeight: 7, 
                                                  indicatorBarColor: selectedColor))
    }
}
```

### Why we built PagerTabStrip!

Nowadays almost every popular iOS app contains a pager view, the benefits are clear, often the app information architecture works best with a pager since it's simple to switch among these "equally relevant" information. Apps like Youtube, Instagram, Spotify, and Twitter use pager views to bring better UX but none of these pagers can be created using the native TabView. Sad, really?

On top of that, we are the creators of XLPagerTabStrip, the most popular pager view in UIKit with almost 7k stars in Github. We also noticed the apple community is constantly asking for a powerful SwiftUI pager view that leverages SwiftUI capabilities such as declarative syntax and the state-driven way to update the UI. Let's be honest, it's hard to find reusable SwiftUI components apart from these developed by Apple, so we embrace the challenge to raise the state of community components and PagerTabStrip is our first step.

### First step with PagerTabStrip

From the beginning, we designed the library to provide the same development experience as using a native Apple component such as TabView. So if you're familiar with TabView, PagerTabStrip will seem super straightforward to use, you just need to add the child view and provide the tabBarInfo view for each one.

This post is just intended to provide a brief introduction about the library so if you're interested in how to use PagerTabStrip I would suggest you take a look at its [github repository readme], you can also run the example project that is contained in PagerTabStrip workspace.

### And we're planning much more...

We believe that PagerTabStrip's first release is very capable and powerful but we plan to enhance it even further. We have plans to integrate every XLPagerTabStrip style among other functionalities. Check out the list of upcoming features in the github repository.

If you liked the library, want to suggest some feature, contribute to the project, or need some help on how to use it please drop us a line on [twitter].

[github repository readme]: https://github.com/xmartlabs/PagerTabStrip
[twitter]: https://twitter.com/xmartlabs
