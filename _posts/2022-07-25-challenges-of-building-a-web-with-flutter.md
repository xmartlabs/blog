---
title: "Challenges of building a web with Flutter"
layout: post
permalink: /blog/challenges-of-building-a-web-with-flutter/
date: '2022-08-13T10:00:00.000-03:00' 
category: development
tags:
  - Flutter
  - Flutter web
  - Web
author_id: felipe
author: Felipe de León

featured_image: /images/building-a-web-with-flutter/featured.png
---
## Lessons learned from a nonconventional approach to flutter web development

Recently a client approached Xmartlabs with the idea of making a platform that achieved excellent results by combining camera usage with [MoveNet](https://www.tensorflow.org/hub/tutorials/movenet), an ML pose detection model. The challenge was to do it fast to ship an MVP that most users could try but make it so that we could reuse the code if we wanted to continue development on other platforms. Flutter appeared as an excellent option to accomplish these needs, so we took on the challenge and started working on a web page with a V1 in mind. However, we found some challenges along the way; this blog is about how we worked around them in case you also bump into similar issues someday.

## Challenge 1: Where is the DOM?

In conventional web development, we always have a tree with nodes representing the elements of our website called **[DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM)**. With Flutter, we don't have exactly what's called a pure DOM. Instead, we have the flutter widgets tree, but all the widgets are drawn into a unique canvas element. This has some inconveniences since you are not able to inspect elements that are not present in the DOM, and debugging gets complicated. A **tool that helped us overcome this was the Flutter [DevTools](https://docs.flutter.dev/development/tools/devtools).** But we could not directly fix some issues, like how bad this impacts SEO.

```html
<html>
    <head>...</head>
    <body flt-renderer="canvaskit (auto-selected)" flt-build-mode="release" spellcheck="false" style="...">
        <flt-glass-pane style="position: absolute; inset: 0px; cursor: default;">
            <flt-scene-host aria-hidden="true" style="pointer-events: none;">
                <flt-scene>
                    <flt-canvas-container>
                        <canvas width="2400" height="1912" style="..."></canvas>
                    </flt-canvas-container>
                </flt-scene>
            </flt-scene-host>
        </flt-glass-pane>
    </body>
</html>
```

<p style="color:gray; font-size:80%; font-style: italic;" align="center">
The result of inspecting a web made in Flutter, as you can see there is only a canvas and thats it.
</p>

## Challenge 2: Works in debug, but does it in prod?

Dart has two compilers for the web, one that supports debugging and hot reloading called `dev_compiler`, and other `dart2js` that focuses on code optimization. Their uses are obvious, one for development and one for release code. But in our experience, some things that work in one don’t necessarily work in the other, so **running the app in release mode** has become a must in the development cycle to test the app.

 ```dart
  @override
  Widget build(BuildContext context) => Column(
        children: [
          Positioned(
            child: Text('This text is positioned'),
          )
        ],
      );
```

<p style="color:gray; font-size:80%; font-style: italic;" align="center">This should never work but it does in debug not in release.</p>

## Challenge 3: Accessing hardware from Flutter

All platforms have different ways to access their hardware capabilities, and the web is not the exception to this rule, there are standards defined in MDN for [MediaDevices](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices). **The [`html`](https://api.dart.dev/stable/2.17.6/dart-html/dart-html-library.html) package comes to the rescue here** and allows us to use some of these capabilities for the web in Flutter, but it makes the code platform oriented.

```dart
 var videoConfig = {
    'audio': false,
    'video': {
      'facingMode': 'user',
      'frameRate': {
        'ideal': 60,
      }
    }
  };

await window.navigator.mediaDevices?.getUserMedia(videoConfig);
```

<p style="color:gray; font-size:80%; font-style: italic;" align="center">This code can be used only on the web and would make the app crash on mobile.</p>

## Challenge 4: Using Html components with Flutter

Widgets allow us to do plenty of UI work, but what happens if we want to do more specific things, like draw something on a custom canvas in the DOM or play a live feed of the camera? Once again, **the `html` package** comes to the rescue helping us use platform-specific capabilities like placing a canvas or a div element on the screen.

Having said that, we must ensure to **correctly use those elements** without getting a weird user experience.

- **HTML elements are not like Flutter. When changing states, they can behave weirdly**: From size changes to nonworking HTML code, elements don't interact well when updated constantly. For example, a camera element that's being updated all the time without need can result in the image blinking continuously.
![camera-example.gif](/images/building-a-web-with-flutter/camera-example.gif)
- **HTML and Flutter lifecycle are separated:**
We must be especially careful with this point since not correctly managing web elements can be linked to dead dart code, making the app crash by accessing variables or components that are no longer available.

To avoid this kind of behavior, HTML elements should be declared at the top of your widget trees or register its **`viewFactory` with a unique random key each time you want to recreate the widget.**

```dart
  // HTML Video element example 
  // This id denomination can led to unexpected behavior:
  var videoElementId = 'video_element';
  // this cannot since the id will be different each time its recreated
  var videoElementId = 'video_element_${DateTime.now().millisecondsSinceEpoch}'; 

  // ignore: undefined_prefixed_name
  ui.platformViewRegistry.registerViewFactory(videoElementId, (int viewId) {
    eventListener = (event) {
     // Do stuff with the camera stream
     webcamVideoElement.removeEventListener('loadeddata', eventListener);
    };
    _webcamVideoElement.addEventListener('loadeddata', eventListener);
    return _webcamVideoElement;
  });
```

<p style="color:gray; font-size:80%; font-style: italic;" align="center">An example of a view factory registration for a video element.</p>

## Challenge 5: Using js code in Dart

While there are plenty of packages that port js libraries to Dart, sometimes you need more custom functionalities. Making use of js code from Flutter has been an easy task for the most part, but there are some considerations to have:

- If you need to wait for a promise in js to end, you will have to **wrap it as a dart** future using the **[`js_util`](https://api.flutter.dev/flutter/dart-js_util/dart-js_util-library.html) package.**
- If you need to send a callback to something implemented on js, you will need to **wrap all your callbacks in the `allowInterop` function.**
- One common thing in js is to call methods with fewer attributes than they have. This is impossible when we combine js with Dart since all parameters must be stated. In some cases, this can lead to changes you must make on the js side.

## Challenge 6: Browser support

Testing in different browsers has become a problem since sometimes the widgets are drawn differently depending on the browser, fonts are not displayed properly or images are just displayed with notable decrease in their quality. If to this we add that you can debug only in Chrome, it can become a real headache. You can also find an issue in web developments here; not all browsers implement conventions the same, and you have to consider this when using the `html` package.**You could end up writing down specific browser code.**

## Conclusions

So far, so good. Flutter has successfully allowed us to develop an app that is not your most conventional use case, but as with all great things, there are some downsides, and Flutter web is no exception to the rule. It does great with simple and basic apps, but when complexity arises, there are some things we have to be conscious about.

The `html` package comes in handy, but it makes code platform-specific. Moving this code into plugins could be helpful to make cleaner code, but it will add a boilerplate, and you would have to maintain the plugins you need.

Slight differences (or even outright completely different) in implementations of features by the browsers can be a pain; even though this is not an issue with Flutter directly, it carries on to Flutter sometimes having to do browser-specific code.

Other than that, Flutter achieves its purpose and allows us to reuse the majority of the developed code between platforms and with the level of complexity that we intended to build we are very satisfied with the decision we made.
