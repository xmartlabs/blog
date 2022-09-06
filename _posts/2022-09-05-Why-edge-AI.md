---
layout: post
title: When and why should you go for AI on the edge?
date: '2022-09-05T10:00:00.000-03:00'
author: Mathias Claassen
tags: [Machine Learning, Edge, Mobile]
author_id: mathias
category: machine-learning
featured_image: /images/why-edge-ai/AI_on_the_edge.png
permalink: /blog/why-edge-ai/
---

# When and why should you go for AI on the edge?

AI on the Edge, or Edge AI, is a concept that people often disregard in their projects without an idea of how powerful it can be.
In this blog, I'll explain what edge AI is, its advantages and weaknesses (and how to work around them), its role compared to cloud AI, and when you should definitely go for it.

## What is Edge AI?

Edge AI refers to when an ML model is deployed to run client-side.
This can be on a device the clients regularly use, like mobile phones or desktop computers, often referred to as on-device ML.
Alternatively, the model could be deployed on smaller specialized GPUs inside the client’s infrastructure, such as Nvidia’s Jetson Nano or Google’s Coral Dev Board.

Mobile phones include increasingly powerful GPUs or specialized ML engines, like Apple’s Neural Engine. Similarly, specialized edge GPUs are available for reasonable prices (around $100), and their variety increases yearly.
So we can say that most edge devices can deliver good performances on certain models.

While there are different use cases for each of these alternatives, the reasons why you should go for any of them are similar.
However, they are not suited to all use cases. So if you want to know if this applies to your situation, keep reading!

<figure>
<img src="/images/why-edge-ai/jetson_nano.jpeg" alt="Nvidia Jetson Nano" width="60%">
<figcaption align = "center"><b>Nvidia Jetson Nano</b></figcaption>
</figure>
<!-- ![Nvidia Jetson Nano](/images/why-edge-ai/jetson_nano.jpeg) -->

## Why should you care about Edge AI?

There are multiple **advantages** of deploying your ML model client-side.

#### **Privacy**

Running your model on a client's device means the input data never leaves the client. This can be a dealbreaker in a world that's increasingly more conscious about their privacy. Privacy becomes even more critical when dealing with sensitive information that can be embedded in images, videos, or some other form of personal data. Face recognition might be a good example.

#### **Low latency**

There is no need to send data to the server and back. This is especially useful when processing videos, for example. Suppose you want real-time feedback on the camera feed. In that case, you can process that directly on-device instead of streaming the video to your servers, processing it there (possibly in a queue with those from other users), and sending the results back.

#### **Cost**

Usually, there are no costs associated with deploying to mobile phones or desktops. There is a one-time setup cost when deploying models to edge devices like the Jetson Nano if that is not already in place. However, the cost of deploying and running models in the cloud can grow considerably, especially if your user base grows.

In terms of development cost, deploying a model on the edge has an added cost of converting models to formats suitable for mobile, web frontend, or edge GPUs. But this process is more streamlined and straightforward by the day. It will be more or less complicated depending on the model architecture and performance requirements.

#### **Models specialized in user data**

An interesting feature made available when deploying a model to the client is that you could potentially fine-tune the model using the data from that specific user. This is possible when using CoreML models in iOS, for example, and could also be implemented on Jetson or Coral devices.

#### **Working offline**

There is no need for an internet connection when the model is deployed locally in its entirety. That can be an advantage in certain use cases where availability is critical.

## What are the disadvantages or limitations of Edge AI

Obviously, some limitations must be kept in mind when deciding whether to go for AI on the edge. Here we show a list of the main limitations, with some ideas on how you can work around them.

#### Less resources

Edge devices probably won't have a GPU as powerful as you can get in the cloud. The same can be said about RAM, storage, and CPU. Also, scaling up these resources is impossible, but this won't be a problem for mobile phones or desktops as each device will have to handle only its own workload.

The main problem with this is model size. Newer models tend to be more prominent in size, and you can hardly deploy models bigger than 100Mb on mobile phones or desktops. While edge GPUs might run slightly bigger models, many models nowadays weigh in the GBs.

You can apply several techniques to reduce the model size without losing much accuracy, for example, converting a model to use half precision or quantization (which will use int8 or smaller). You can also do model pruning or knowledge distillation to reduce the size more drastically. You could also look for a smaller model architecture which might not be much less performant. Applying these will come with added development costs (see below), although current frameworks constantly improve support for them.

Another problem, for mobile phones, in particular, is that if you make extensive use of their GPU, they might overheat, which is not a great user experience.

#### Extra development cost

When you deploy your model on the edge, you will have an additional development step to optimize the model for that platform (for example, with TensorRT) or convert it to a different format like TensorFlow Lite or CoreML. After this conversion, you will need to retest the model to make sure it still works as intended. The conversion will be straightforward for some models, but it can be a hassle for others. One possible problem is that most mobile or web frontend ML frameworks have a reduced subset of layers they support compared to their server counterparts. This means you might have to implement some layer in that framework or tweak your model architecture. Sometimes layers might be supported but only on CPU.

When going for web, you will most likely use TensorflowJS, while for mobile, you will consider Tensorflow Lite, Pytorch Mobile, or CoreML (iOS only). Pytorch Mobile is a newer framework than the others, and, as of 2022, it has very limited support for layers, especially to run on GPU. This means you will probably prefer the others for now. You can review our blogs about converting models from [TF lite to CoreML](https://blog.xmartlabs.com/2019/11/22/TFlite-to-CoreML/), as well as a comparison between [CoreML and Bender](https://blog.xmartlabs.com/blog/how-to-get-the-best-performance-for-ml-models-on-ios/).

There are also some additional challenges when you plan to deploy an automated pipeline following MLOps best practices. Model testing, monitoring, and continuous deployment will be different from cloud setups. We will explore this more in-depth in a future blog post. Stay tuned.

If you need help with this process, don't hesitate to [drop us a line](mailto:hi@xmartlabs.com).

### Comparing Edge AI vs Cloud AI

|  | Edge AI | Cloud AI |
| --- | --- | --- |
| Deployment cost | Free / One-time payment | It depends (but GPUs on the cloud are expensive if they need to run for a long time) |
| Works offline | Yes | No |
| Latency | Just inference time of the model | Inference time of the model + time to send data to server and back + queue wait time (depending on user base) |
| Privacy | Sensitive data doesn’t leave the client’s device or infrastructure | All data is sent to a cloud provider. You can still choose not to store any sensitive data, but the user does not know what you do with it. |
| Model size  | Small (for mobile and web, you might want to stay < 100MB) | Large |
| Compute power | Limited | Can scale up |

## Use cases: When should you consider Edge AI?

Given the advantages and limitations of deploying your models on the edge, you might wonder what the best choice for your use case is. As mentioned above, edge AI is especially suited to certain use cases. If the added benefit of any of the mentioned advantages is important to you, then you should consider it. However, if you know that your model won't fit into a client's device and techniques to reduce its size will be too costly for its accuracy, then this is not for you.****

Video processing is especially suited to edge processing when the content might be privacy sensitive while also creating heavy network usage, which must be handled server-side. In this case, you should consider at least a hybrid approach, where the video is processed in a model client-side, and the results of that model are then processed further on your cloud.

The hybrid approach might also be suited to other use cases where privacy is critical, and you are processing data in multiple steps.

Another use case is when your target users live in areas with connectivity issues, and the availability of your service is essential. In this case, deploying your model in a mobile app, for example, can potentially allow a bigger set of features to be available at any time.

We have built several mobile apps, which include ML models. [DreamSnap](https://dreamsnap.xmartlabs.com) lets your camera feed look like an artist’s painting in real-time. To do this efficiently in real-time with low latency, we needed to deploy the model on the mobile app itself. While building DreamSnap, we open-sourced [Bender](https://github.com/xmartlabs/Bender), a framework to make running efficient ML workloads on an iOS GPU seamless.

We also built an app that converts [voice messages to text](https://apps.apple.com/us/app/voice-message-to-text/id1532055277) so that you can read what a friend sent you while you are unable to listen for a moment. This app uses Apple’s SpeechRecognition, which can run on-Device or in the cloud, depending on configuration or whether the user has a good internet connection.

## Conclusions

Deploying an ML model on edge has advantages and limitations, and whether you should consider it depends on your use case. Edge processing power is growing fast, and the latest smartphones have great potential in this aspect. Popular ML frameworks are also increasing and improving support for edge deployment.

There is some specific knowledge to acquire when embarking on this journey, but there are people like us who [can help you with that](mailto:hi@xmartlabs.com). You can see more of what we have done [here](https://xmartlabs.com/machine-learning).