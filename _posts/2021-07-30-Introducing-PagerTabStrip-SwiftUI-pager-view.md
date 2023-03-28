---
layout: post
title: Introducing PagerTabStripView! - Finally a PagerView in pure SwiftUI
date: '2021-08-06T10:00:00.000-03:00'
author: Martin Barreto
tags: [Xmartlabs, PagerTabStripView, SwiftUI PagerView, XLPagertabStrip]
author_id: mtnBarreto
category: [development, mobile-development, ios-development]
featured_image: /images/pager-swiftui/Twitter-1.png
social_image: /images/pager-swiftui/Twitter-1.png
twitter_image: /images/pager-swiftui/Twitter-1.png
permalink: /blog/Introducing-PagerTabStripView-PagerView-in-SwiftUI/
---

<p style="text-align:left;width:100%">
<img src="/images/pager-swiftui/Blog-skinny.png" alt="Project banner">
</p>

We're incredibly thrilled to announce [PagerTabStripView](https://github.com/xmartlabs/PagerTabStripView), the most powerful pager view entirely written in SwiftUI.

Creating a production-ready pager view could take several hours, even days, for an engineering team. Apple recently introduced a pager version on top of its native TabView, trying to address the growing demand for pager views, but it lacks flexibility. It is pretty much the TabView with swipe gestures. Its customization level is so limited that it ends up not working in most cases.

What if I told you that with the PagerTabStripView, you can create those pagers in a matter of minutes and not days. This exactly was our vision when we started to build this flexible yet powerful library.

Let's move on and see how you can build a sophisticated pager view in a matter of seconds, a code snippet is worth more than a thousand words 😂.

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

# Why we built PagerTabStripView?

Nowadays, almost every popular iOS app contains a pager view, the benefits are clear. Often, the app information architecture works best with a pager since it's simple to switch among these "equally relevant" information. Apps like YouTube, Instagram, Spotify, and Twitter use pager views to bring better UX, but none of these pagers can be created using the native TabView. It's an unfortunate thing, but it's true.

On top of that, we are the creators of XLPagerTabStrip, the most popular pager view in UIKit with almost 7k stars in GitHub. We also noticed the Apple community is constantly looking for a powerful SwiftUI pager view that leverages SwiftUI capabilities such as declarative syntax and the state-driven way to update the UI. Let's be honest, it's hard to find reusable SwiftUI components apart from these developed by Apple, so we embraced the challenge to raise the state of community components, and PagerTabStripView is our first step.

# What does "In Pure SwiftUI" mean?

From the beginning, we designed the library to provide the same development experience as using a native Apple component such as TabView. So if you're familiar with TabView, PagerTabStripView will seem super straightforward to use; just add the child views and provide the pagerTabItem view for each one.

**PagerTabStripView defines the UI using the elegant SwiftUI declarative approach.** From day one, we banned collections of views to updates the UI.

```swift
PagerTabStripView() {
    MyFirstView()
        .pagerTabItem {
            TitleNavBarItem(title: "Tab 1")
        }
    MySecondView()
        .pagerTabItem {
            TitleNavBarItem(title: "Tab 2")
        }
    if User.isLoggedIn {
        MyProfileView()
            .pagerTabItem {
                TitleNavBarItem(title: "Profile")
            }
    }
}
```

**We never interface with UIKit, which means we don't import UIKit anywhere.** No usage of `UIViewRepresentable` and `UIViewControllerRepresentable` protocols.

**PagerTabStripView interface looks like native component SwiftUI interfaces.** It uses pretty much the same syntax and approach to customize the pager view as native TabView.

```swift
PagerTabStripView(selection: $selection) {
    ForEach(1...10, id: \.self){
        MyPagerChildView()
            .pagerTabItem {
                TabInfoView(title: "Page Info Title \($0)")
            }
    }
}
```

**State variables and conditional blocks are used to declaratively update the shown pages of the pager view.** Of course, you can also use SwiftUI `ForEach` (as the example above shown) to provide child views on demand from an underlying collection if you wish so.

**Associated views to select a page by tap gesture are declaratively defined using a View Modifier on each child page view.**

```swift
PagerTabStripView(selection: $selection) {
    ForEach(1...10, id: \.self){
        MyPagerChildView()
            .pagerTabItem {
                VStack {
                    Text("Page \($0)")
                    .foregroundColor(theme.textColor)
                    .font(.subheadline)
                }
                .frame(maxWidth: .infinity, maxHeight: .infinity)
                .background(Color.white)
            }
    }
}
```


And many more you will figure out down the road 😜!


# And we're planning much more...

We believe that PagerTabStripView's first release is super capable, but we plan to further enhance it. We have plans to integrate every XLPagerTabStrip [style](https://github.com/xmartlabs/XLPagerTabStrip#pager-types), among other functionalities.

As this post is just intended to announce the library, if you're interested in using the PagerTabStripView, I suggest you look at its [GitHub repository readme]. You can also run the example project, contained in the PagerTabStripView workspace, which showcases different pager views.

<table>
  <tr>
    <th><img src="/images/pager-swiftui/twitterStyleExample.gif" width="90%"/></th>
		<th><img src="/images/pager-swiftui/LogOutExample.gif" width="90%"/></th>
    <th><img src="/images/pager-swiftui/instagramStyleExample.gif" width="90%"/></th>
  </tr>
</table>

If you liked the library, want to contribute to the project, or need some help using it, please drop us a line on [twitter], comment down below, or open an issue or a pull request.

That's all, folks! Hope the library saves you the day sometime! See you in the next post!

[GitHub repository readme]: https://github.com/xmartlabs/PagerTabStripView
[twitter]: https://twitter.com/xmartlabs
