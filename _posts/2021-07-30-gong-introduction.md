---
layout: post
title: Kickstart your Android Project with Gong App Template
date: 2021-08-04 10:00:00
tags: [Android App Template, Android Base project, Android Compose Base Project, Xmartlabs Android App, Jetpack Compose App Template, Jetpack Compose Base Project, Android Development, Kotlin Development]
category: development
author_id: sante
show: true
featured_image: /images/gong-introduction/banner.png
social_image: /images/gong-introduction/bannerSocial.png
twitter_image: /images/gong-introduction/bannerTwitter.png
permalink: /blog/kickstart-your-new-android-project-with-gong-app-template/
---

<p style="text-align:left;">
<img src="/images/gong-introduction/bannerInterno.png" alt="Project banner">
</p>

Starting a software project is not an easy task and Android is no exception, there's a bunch of complex decisions to make such as code conventions, libraries, continuous integrations, environments management, app architecture, and best practices just to mention a few.

Each time we kick off a project we're forced to write this boilerplate code and typically we end up using the same project structure, libraries, code style, helpers over and over again, which is good to be consistent in the form we build apps but it's also a naivete issue to spend time building the same base project.

In this blog post, we introduce Gong, the Android App Template we use to kickstart every Android app we build. Gong was fully developed and it's actively maintained by our Android team, and it's the result of years of experience in creating well-written and maintainable Android code using Kotlin and recently Jetpack Compose.


# What exactly is Gong?

[Gong][gong] is our Android App Template to effortlessly kickstart Android projects and get us quickly ready to implement product functionalities. By using Gong, in a matter of seconds you can create the base project for your android app, the same base project we use at Xmartlabs, you only have to clone the repo and run a provided script to set up the project name, namespace, and few more data about your particular app.

Gong is fully written in [Kotlin][kotlin] and it leverages the language's capabilities and modern syntax (if you're still programming Android apps in [Java][java], give Kotlin a try, you won't regret it :wink:). It also uses [Jetpack Compose][compose]: the new declarative toolkit for creating UI in Android.

Apart from providing a top-notch architecture and several out of the box project development solutions and tools that speed up Android app development, Gong enforces the usage of the same code conventions, adopt the same project structure, follow platform best practices, and use pretty much the same third-party libraries throughout the whole Android team.

Gong was intended to help Android teams to adopt elegant, clean, and maintainable Android code, use state-of-the-art components and libraries, and quickly get into coding valuable app functionality with virtually no effort and in no time.


# Kickstarting your project using Gong

Creating your app base code using Gong is super simple, you just have to clone the Gong repo and run a script that prompts you to set up your project information such as project and package name! That's all!

If you are interested, there is a step-by-step guide on how to initialize the script and provide such information on Gong's Github readme page.

Once you provide the project's information, Gong automatically renames and refactors the template code according to your naming conventions (you never need to do any manual refactoring). You can even provide your Git remote URL so the project is set up pointing to your remote repository.

Let's see how easy it's below:

<p style="text-align:center;">
<img style="width: 100%" src="/images/gong-introduction/howto.gif" alt="How to start using it">
</p>

# The Generated base Android project

Once the script execution finishes, you can open the generated Android project, which was named <YourProjectName>.xyz.

Checking out the generated project, you can find a well-constructed package structure to organize your files storing them where they belong. It also provides you with common build variants (dev, prod) ready to use.

<p style="text-align:center;">
<img src="/images/gong-introduction/projectTree.png" alt="Generated project tree"/>
</p>

- **Data:** This should be the place for all your models and data sources (local or remote), making sure to organize the related ones inside a package to keep the structure clean and understandable.
Gong uses the Repository pattern to provide data to where it's needed.

- **Device:** Here you get a base definition for dependency injection using [Koin][koin] where you can place all your modules, a place for Kotlin extensions and a logger definition.
Also, as the project uses Compose's declarative approach for UI, you get a definition of a template class called `ProcessState` which is used to manage the state required by the Model-View-Intent (MVI) architecture that's used.

- **Domain:** In this package you get the aforementioned repositories as well as a template use case definition accompanied by a few implementation examples.

- **UI:** This package is meant to have all your user interface related elements such as composables, classic views, fragments and activities.
Besides, we provide an extension to Compose's proposed theme management which gives you more flexibility to manage all your color palettes, fonts and shapes.
It also gives you an easy way to add more elements to fit your definition of theme.
For more information about this, our team released another [blogpost][mirland] about this some time ago.


# Final thoughts

If you liked what's presented in this blog post, head to its [GitHub site][gong] to learn more about it from the documentation and, why not, start your Android project using Gong, reaping all of its benefits.

Of course, we are open to contributions so feel free to create issues with proposals or submit pull requests to incorporate improvements!

Don't hesitate to contact our team for any help or if you have an app idea to develop!

Finally, we want to say thank you to [everyone][contributors] who helped create and maintain this project!

[gong]: https://github.com/xmartlabs/gong
[mirland]: https://blog.xmartlabs.com/blog/extending-material-theme-in-jetpack-compose/
[kotlin]: https://kotlinlang.org/
[java]: https://java.com
[koin]: https://insert-koin.io/
[contributors]: https://github.com/xmartlabs/gong/graphs/contributors
