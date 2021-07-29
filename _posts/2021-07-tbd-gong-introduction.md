---
layout: post
title: Kickstart your new Android project with Gong base project 
date: 2021-05-11 10:00:00
tags: [Jetpack Compose, Android, Android Base Project]
category: development
author_id: sante
show: false
featured_image: /images/extending-material-theme-in-jetpack-compose/banner.jpeg
social_image: /images/extending-material-theme-in-jetpack-compose/banner_social.jpeg
twitter_image: /images/extending-material-theme-in-jetpack-compose/banner_twitter.jpeg
permalink: /blog/extending-material-theme-in-jetpack-compose/
---
# What's Gong?
​
Starting a software project is no easy task and Android is no exception, there's a lot of boilerplate code to write and decisions to make about the architecture of the app. Each  time we started a new project we had to make a lot of decisions and get the team on the same page. That's why we created [Gong][gong], our Android base project, to kickstart the first steps of the process and get us ready to implement features effortlessly. All the features included in Gong are the product of research and experience about what works best while being readable and easy to mantain and extend. 
​
Gong is written in the latest version of [Kotlin][kotlin] (if you are programming for Android in [Java][java], give Kotlin a try, you won't regret it :wink:) to use all the best features the language offers, and uses [Jetpack Compose][compose] the new and modern declarative way of creating UI in Android using only Kotlin.
​
In short, Gong is a base project which gives you a good structure, architecture, good practices and modern features and toolkits with virtually no effort and in no time.
​
# How can you kickstart your project using Gong?
Beginning your project with Gong couldn't be easier, you just have to run a script! 
​
If you head to the project's GitHub page, in the readme you will find a command which lets you execute the initialization script. By doing that, you will be prompted to submit your project name as well as your package name (so your project is correctly named and you don't have to do any manual refactoring). Also, you can optionally provide a Git remote URL so the project can be set up pointing to your remote repository.
​
You can see how easy it is here:

​
![How to start using it][howto]
​
# What do you get when running the script?
The script gives you a well constructed package structure to organize your files storing them where they belong. Also, you get common build variants predefined and available to use (dev, prod).

​
![Generated project tree][projectTree]
​

- Data: This should be the place for all your models and data sources (local or remote), making sure to organize the related ones inside a package to keep the structure clean and understandable. Gong uses the Repository pattern to provide data to where it's needed. 
​

- Device: Here you get a base definition for dependency injection using Koin where you can place all your modules, a place for Kotlin extensions and a logger definition. Also, as the project uses Compose's declarative approach for UI, you get a definition of a template class called `ProcessState` which is used to manage the state required by the Model-View-Intent (MVI) architecture that's used.


- Domain: In this package you get the aforementioned repositories as well as a template use case definition accompanied by a few implementation examples. 
​

- UI: This package is meant to have all your user interface related elements such as composables, classic views, fragments and activities. Also, we provided an extension to Compose's proposed theme management which gives you more flexibility to manage all your color palettes, fonts and shapes, while also giving you an easy way to add more elements to fit your definition of theme. For more information about this, our team released another [blogpost][mirland] about this some time ago.
​
# Try it out!
If you liked what's presented in this blogpost, head to its [GitHub site][gong] to learn more about it from the documentation and, why not, start your Android project using Gong, reaping all of its benefits. Of course, we are also open to contributions and opinions so feel free to create issues with proposals or improvements!
​
​

[gong]: https://github.com/xmartlabs/gong
[mirland]: https://blog.xmartlabs.com/blog/extending-material-theme-in-jetpack-compose/
[kotlin]: https://kotlinlang.org/
[java]: https://java.com
[howto]: /images/gong-introduction/howto.gif
[projectTree]: /images/gong-introduction/projectTree.png
