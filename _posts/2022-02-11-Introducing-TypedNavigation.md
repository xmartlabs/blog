---
layout: post
title: Introducing TypedNavigation
date: '2022-02-11T10:00:00.000-03:00'
author: Felipe de León
tags: [Android, Compose, Jetpack Compose, Navigation]
author_id: felipe
show: false
category: android-development
featured_image: /images/taskflow/taskflow-blogpost.jpg
permalink: /blog/computer-vision-and-object-detection-use-case/
---

With the introduction of Jetpack Compose Android development changed drastically; among this changes navigation was not the exception. With (compose navigation)[https://developer.android.com/jetpack/compose/navigation] we move away from the old XML based navigation graph to a new declarative paradigm in Kotlin. This new way of declaring navigation lacked typed checked methods, furthermore one have to cast each attribute to the original type increasing the boilerplate code. **TypedNavigation** is a lightweight library built over the new copmpose naviagtion, that aims to solve this problem by providing a set of models and extensions that would help you navigate with type checking and avoid boilerplate!


### Type checked navigation

**TypedNavigation** defines a set of models that are abstractions of a destination with its attributes from none up to 5, the intention behind this is to set a source of truth for attributes, deeplinks and other things that will be useful when navigating to a screen. The following shows an example of a `Router` an object that will contain all navigation information.



```kotlin
object Router {
    val default = TypedNavigation.E("default")
    val home = TypedNavigation.A2("home", NavType.StringType, NavType.IntType)
    val example = TypedNavigation.A3("example", NavType.StringType, 
    NavType.StringType, NavType.StringType, listOf { a1, a2, a3 ->
            "www.example.com/$a1/$a2/$a3"
        }
        )
}
```
The types `E, A1, ... A5` represent navigation with attributes E being the navigation with none attributes and `An` being navigation with n. When declaring a destination you must add the types used in the navigation and optionally the deeplinks that will navigate upon them if necessary.

You still will have to state the navigation in your activity but now you will be able to access the attributes with their correct type.

```kotlin
setContent {
    val navigationController: NavHostController = rememberNavController()
    NavHost(navController = navigationController, startDestination = Router.default.url) {
        composable(Router.default) {
            Default(navigationController = navigationController)
        }
        composable(Router.home) { a1 : String?, a2 : Int ->
            Home(a1, a2)
        }
        composable(Router.example) { a : String?, b : String?, c : String? ->
            Example(a, b, c)
        }
    }
}
```

Finally you will be able to navigate directly with the correct typed attributes:

```kotlin
Button(
    onClick = { navigationController.navigate(Router.home.route("example", 5)) },
) {
    Text(text = "Home")
}
```

### Conclusion 

**TypedNavigation** provides a way to navigate between screens with the correct types end to end and without having to cast anything avoiding possible mistakes and boilerplate code. 

If you want to see a sample app or the source code you can access the GitHub [repository](https://github.com/xmartlabs/TypedNavigation)

<div>
<a data-mode="popup" data-hide-footer="true" target="_blank" href="https://form.typeform.com/to/D1PhDJIR" class="button is-nav ipad-hidden typeform-share w-inline-block header-getintouch" style="opacity: 1;">
  <div class="button-text no-pointer">Let's talk</div>
</a>
</div>
<br />
<br />

