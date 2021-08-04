---
layout: post
title: Kickstart your Android Project with Gong Base Project
date: 2021-08-04 10:00:00
tags: [Android App Template, Android Base project, Android Compose Base Project, Xmartlabs Android App, Jetpack Compose App Template, Jetpack Compose Base Project, Android Development, Kotlin Development, Jetpack Compose, Android, Kotlin]
category: development
author_id: sante
show: true
featured_image: /images/gong-introduction/banner.png
social_image: /images/gong-introduction/bannerSocial.png
twitter_image: /images/gong-introduction/bannerTwitter.png
permalink: /blog/kickstart-your-new-android-project-with-gong-base-project/
---

<p style="text-align:center;">
<img src="/images/gong-introduction/bannerInterno.png" alt="Project banner">
</p>

Starting a software project is not an easy task, and Android is no exception.
There's a bunch of complex decisions to make, such as code conventions, app architecture, frameworks, libraries, continuous integrations, and best practices, to mention a few.
That's why we created [Gong][gong], to consolidate all our discussions and research in one base project that we could use to give a boost to our productivity, and give other teams a solid base from which to start their projects.

This blog post introduces Gong, the Android App Template we use to kickstart every Android app we build.
Gong results from years of experience in creating well-written and maintainable Android code using Kotlin and, recently, Jetpack Compose, and our Android team actively maintains it.


# What exactly is Gong?

[Gong][gong] is our Android App Template to effortlessly kickstart Android projects and get us quickly ready to implement product features.
By using Gong, in a matter of seconds, you can create the base project for your android app, the same base project we use at Xmartlabs.

Gong is entirely written in [Kotlin][kotlin], and it leverages the language's capabilities and modern syntax (if you're still programming Android apps in [Java][Java], give Kotlin a try, you won't regret it 😉).
It also uses [Jetpack Compose][compose], the new declarative toolkit for creating UI in Android.

In short, Gong is a base project which gives you a good structure, well-constructed architecture, good practices, and modern features and toolkits with virtually no effort and in no time, so you can start implementing features right away.


# Kickstarting your project using Gong

Creating your app base code using Gong is super simple. You just have to run one command that fetches and executes a script that asks for your project information, such as project and package name. That's all!

The command is available on [Gong's Github readme page][setup], along with instructions to do the setup manually if you prefer to do so.

Once you provide the project's information, Gong automatically renames and refactors the package and class names containing `Gong` replacing it for your project name (you don't need to do any manual refactoring).  
You can even provide your Git remote URL to set up your project pointing to your remote repository.

Let's see how easy it's below:

<p style="text-align:center;">
<img style="width: 100%" src="/images/gong-introduction/howto.gif" alt="How to start using it">
</p>

# The Generated base Android project

Once the script execution finishes, you can open the generated Android project in Android Studio (or the ide of your preference).

Checking out the generated project, you can find a well-constructed package structure to organize your files storing them where they belong. It also provides you with common build variants (dev, prod) ready to use.

<p style="text-align:center;">
<img src="/images/gong-introduction/projectTree.png" alt="Generated project tree"/>
</p>

- **Data:** The package for all your models and data sources (local or remote). Make sure to organize your models and data sources according to its relation to keep the structure clean and understandable. Gong uses the Repository pattern to provide data to where it's needed.

- **Device:** Here, you get a base definition for dependency injection using [Koin][koin] where you can place all your modules, Kotlin extensions, and logger definitions. Also, as Gong uses Compose's UI declarative approach, it provides a template class called `ProcessState`, which manages the state required by the Model-View-Intent (MVI) architecture.

- **Domain:** In this package you get the aforementioned repositories as well as a template use case definition accompanied by a few implementation examples.

- **UI:** This package is meant to have all your user interface-related elements such as composables, classic views, fragments, and activities. 
Besides, we provide an extension to Compose's proposed theme management, which gives you more flexibility to manage all your color palettes, fonts, and shapes. It also gives you an easy way to add more elements to fit your definition of theme. For more information about this, our team released another [blog post][mirland] about this some time ago.


# Final thoughts

In this blog post, we introduced our Android base project, the base code we use to kick off every Android project rapidly.
If you liked it and want to know more about using Gong in your own projects, please head to its [GitHub documentation][gong].

Of course, we are open to contributions, so feel free to create issues with proposals or pull requests to incorporate improvements!

If you have an app idea to develop, don't hesitate to contact us! We're more than happy to help!

Finally, we want to thank [everyone][contributors] who helped create and maintain this project! 💪 🚀

[gong]: https://github.com/xmartlabs/gong
[mirland]: https://blog.xmartlabs.com/blog/extending-material-theme-in-jetpack-compose/
[kotlin]: https://kotlinlang.org/
[java]: https://java.com
[koin]: https://insert-koin.io/
[contributors]: https://github.com/xmartlabs/gong/graphs/contributors
[compose]: https://developer.android.com/jetpack/compose
[setup]: https://github.com/xmartlabs/gong#setup
