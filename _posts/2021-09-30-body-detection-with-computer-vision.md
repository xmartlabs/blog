---
layout: post
title: Body Detection with Computer Vision
date: '2021-09-28T10:00:00.000-03:00'
author: Valentina Bianco
tags: [Pose Estimation, Body Segmentation, Human Detection, Machine Learning, Computer Vision]
author_id: vale
show: true
category: machine-learning
featured_image: /images/bender-is-the-best/featured.jpg
permalink: /blog/computer-vision-techniques-for-body-detection/
---

Being able to automatically infer human bodies in images has opened avenues for an array of real-life applications.

Everyone, in one way or another, has used these technologies. Whether you've used zoom (and almost everyone has in the past two years 😒) and played around a bit [with filters](https://twitter.com/lawrencehurley/status/1359207169091108864?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1359207169091108864%7Ctwgr%5E%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fwww.buzzfeed.com%2Fhannahmarder%2Fhilarious-quarantine-zoom-fails) and with replacing your background, or if you have a fitness app that keeps track of the exercises and how you're performing them, or perhaps you have security cameras at home that alert you when they detect humans.

To achieve this, computer vision has expanded into sub-branches that you might have heard of: Image segmentation and classification, object detection, tracking, human pose estimation, etc.

With all this jargon and terminology, it's easy to get lost. This blog post aims to bring clarity while expanding a bit more on body detection through computer vision.

First, we'll go back to basics and expand a bit on computer vision and the models that comprise it. Then we'll dive into body detection with computer vision, its different approaches, their practical applications, and enumerate the most relevant models in each category taking into consideration benchmark, pros, and cons.

# **What's Computer Vision**

The desire to have a machine or robot think like a human being, to build what is now known as Artificial Intelligence, has been there since before the first computer existed; think Mary Shelley's Frankenstein or Ovid's Pygmalion and his ivory statue.

But if you think about it, what would those creations be if they couldn't see? Sight is a key human sense, we can process about 36,000 bits of information each hour through our eyes. So if we wanted computers to think and reason like human beings, them having the ability to see seems logical. Enter, computer vision.

A sub-study or branch of AI, it aims to provide machines with the capacity not only to see but to *look*. Its aim is for machines to extract valuable information from digital videos and images, and use it to gain a deeper understanding, to think and act as we do.

<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/intro.gif" alt="intro">
</p>
Image: *Bicentennial Man* (1999)

It's no news; we're producing an [enormous amount of data](https://www.internetlivestats.com/) every single day, and it's worth noting that a big percentage of it consists of images and videos (about three billion images are shared every day online). Furthermore, almost every single human being carries a cell phone with them everywhere, which means, they carry a camera at all times and use it constantly. Moreover, the quality of images and videos is improving daily, making it easier to process them. It's only natural that machines take advantage of that huge pool of information.

Engineers have been using computer vision algorithms to automate tasks, like understanding a handwritten letter, identifying cars through their license plate, ensuring humans use face-masks, detect missing objects in gondolas, among others.  

And although it's being broadly studied, it generates a lot of enthusiasm among people (it's expected to reach $48.6 billion by 2022 according to [Forbes](https://www.forbes.com/sites/bernardmarr/2019/04/08/7-amazing-examples-of-computer-and-machine-vision-in-practice/?sh=1cfa13501018)), resulting in huge advances being made over a small amount of time. This is also partly due to companies such as Google, IBM, Microsoft, and Facebook sharing their research through open-source work.

## **How it works**

Computer vision relies basically on two Machine Learning concepts to interpret and understand images and videos:

- **Deep Learning**: In comparison with ML, deep learning can function with minimum human intervention, and with unstructured data sets, it learns more independently. It can process unstructured data in its raw form of text or images. The model will also determine the features that distinguish each data category.
- **Neural Network:** Deep learning relies on neural networks. Inspired by the human brain, it's a general-purpose layered function that can solve a problem by learning by itself from a labeled dataset. When you provide a neural network with many labeled examples of a specific kind of data, it'll be able to extract common patterns between those examples and transform them into a mathematical equation that will help classify future pieces of information.


<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/ML-DeepLearning-Neural Networks-AI.png" alt="ML, DeepLearning, Neural Networks, AI">
</p>
ML, Deep Learning, and Neural Networks are all subfields of AI ([image source](https://lh4.googleusercontent.com/9gORhD6V2G7XBya2mSKVgZitf09o0n97JqQ20yuew4Fo8YfpUT1RO6voAqTOPMQDoorjJtKmI80vLVvltF6JIOK0IOB2F7tA7VgLJxZIUJf-mF2cW80jjPHNtWIZ-FZu2eEC2ePu))

Most common computer vision applications already have a trained deep learning model that engineers can use out of the box. For more complex solutions, engineers need to optimize models or even design a model from scratch, which requires training the algorithm to properly make the predictions, detect events, etc.

Notice that creating and training a Convolutional Neural Network from scratch requires solid machine learning skillsets and considerable quantities of data, but luckily there are plenty already trained models for human detection, pose estimation, and Segmentation, the most used human detection algorithms.

## Computer Vision Techniques

Replicating human sight through a computer can be achieved in several ways depending on your objectives and the type of data you want to obtain. These are the most common techniques that, combined or by themselves, have proved to be effective and are widely used.

### Image Segmentation

It is believed the first thing our brain tends to do when presented with an image is to single out the different objects that comprise it. Segmentation models do this by dividing the image into several parts called segments or objects. These segments are composed of various pixels sharing some common attributes: color, intensity, texture, optical focus. Once they are grouped, a class is assigned to each pixel. Putting together those pixels that actually contain the information needed to be processed saves the model time by ruling out regions of the image with no value. There are two types of image segmentation:

- **Semantic Segmentation:** the process in which pixels are segmented according to its class.
- **Instance Segmentation:** the process that takes part when the image has multiple objects. In which case the objects are masked with different colors and treated as separate entities, all the pixels associated with each object are given the same color.

<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/image-segmentation.jpg" alt="Image Segmentation">
</p>
[Image source](https://ai-pool.com/d/could-you-explain-me-how-instance-segmentation-works)

### Image Classification

Image classification is the process that takes place when a class (i.e. a tag) is assigned to a specific object on the image. Basically, it allows the model to look at a picture and determine whether the object on it is a human being, a dog, a cat, a plant, etc.

To train the models in applying these predefined categories (dog, person, flower), you can [access an array of different datasets](https://imerit.net/blog/top-13-machine-learning-image-classification-datasets-all-pbm/) containing classified images.

If the image contains more than one object, classification is also possible through a multi-level classifier.

### Object Detection

Once you classify all the objects in the image, the next step would be to locate the objects within the image. And that's where object detection comes in. The system can now identify where all the objects are in relation to each other. Think of object detection like image localization *plus* classification for all the objects an image contains.

After applying an OD model your image should look like this, a bounding box around each object in the image with its corresponding class and a score to reflect the confidence that the detection was done correctly.

It used to take 20 seconds to process an image and determine where an object was. Now it's about 1000 times faster (20 milliseconds per image) in a couple of years thanks to contributions such as open-sourced [YOLO](https://pjreddie.com/darknet/yolo/) (bounding boxes and class probabilities simultaneously). This means object detection can be made in real-time.

<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/object-detection.png" alt="Object Detection">
</p>
[Image source](https://medium.datadriveninvestor.com/deep-learning-for-image-segmentation-d10d19131113)

### Object Tracking

So what happens when the object we need to identify is not on a static image but a video? That is, how can we keep track of an object that's moving? This would be the case if, for example, we wanted to identify a certain person or persons in a security camera footage. That's when object tracking comes in to save the day! This process follows a certain object/s over time in the video, and it keeps track of it (or them) through each frame.

You may wonder why you don't just use object detection in every single frame? After all, it's also about identifying the objects and figuring out their location. Well, technically, the answer may be a bit more complex than this, but in short: there's no easy way of connecting multiple objects with each other between the different frames. Also, if the object you're tracking was to go out of camera view for a few frames and come back later, there would be no way of knowing whether it's the same one of a few frames ago.


<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/object-tracking.gif" alt="Object Tracking">
</p>
[Image source](https://towardsdatascience.com/what-even-is-computer-vision-531e4f07d7d0)

Tracking works with objects that change in size, shape, and position depending on the angle they are being captured from if they are moving, the light, etc. Tracking algorithms also contain motion estimation models that understand the dynamic behaviors of objects to predict its trajectory, i.e. the areas where the object is likely to be found in later frames.

### Pose Estimation

Pose estimation is the computer vision technique that detects human figures in images or videos. Typically these models infer seventeen points that represent each key body joint. It's all about the body pose and has nothing to do with human identification, detection, or Segmentation.  

<p style="text-align:center;">
    <img style="width: 100%" src="/images/body-detection-with-computer-vision/pose-estimation.gif" alt="Pose Estimation">
</p>

Image or video streaming can be used as the model input and its output provides information about each body keypoint's position, normally in the form of a 2D space coordinate along with a confidence score between 0 and 1.

There've been several performance improvements around pose estimation. For instance, the Google team is actively working on the [MoveNet](https://blog.tensorflow.org/2021/05/next-generation-pose-detection-with-movenet-and-tensorflowjs.html) project, which provides real-time pose estimation data apart from having a great accuracy rate/score.
