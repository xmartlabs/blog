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
There's a bunch of complex decisions to make, such as code conventions, libraries, continuous integrations, environments management, app architecture, and best practices, to mention a few.

Typically, each time we kick off a project, we use the same project structure, libraries, code style, helpers over and over again, which is good to be consistent in the form we build apps.
But at the same time, it's a naivete issue to spend time implementing the same base project.

This blog post introduces Gong, the Android App Template we use to kickstart every Android app we build.
Gong results from years of experience in creating well-written and maintainable Android code using Kotlin and, recently, Jetpack Compose, and our Android team actively maintains it.


# What exactly is Gong?

[Gong][gong] is our Android App Template to effortlessly kickstart Android projects and get us quickly ready to implement product functionalities.
By using Gong, in a matter of seconds, you can create the base project for your android app, the same base project we use at Xmartlabs.
You only have to clone the repo and run a provided script to set up the project name, namespace, and few extra data about your particular app.

Gong is entirely written in [Kotlin][kotlin], and it leverages the language's capabilities and modern syntax (if you're still programming Android apps in [Java][Java], give Kotlin a try, you won't regret it 😉).
It also uses [Jetpack Compose][compose], the new declarative toolkit for creating UI in Android.

Apart from providing a top-notch architecture and several out-of-the-box app solutions to speed up Android development, it enforces the usage of the same code conventions and project structure, the adoption of the platform best practices, and third-party libraries throughout the Android team.
Gong aims to help Android teams to adopt elegant, clean, and maintainable Android code, use state-of-the-art components and libraries, and quickly get into coding valuable app functionality with virtually no effort and in no time.


# Kickstarting your project using Gong

Creating your app base code using Gong is super simple. You just have to clone the Gong repo and run a script that prompts you to set up your project information, such as project and package name! That's all!

There is a step-by-step guide on initializing the script and providing such information on Gong's Github readme page if you are interested.

Once you provide the project's information, Gong automatically renames and refactors the template code according to your naming conventions (you never need to do any manual refactoring).  
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
