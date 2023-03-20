---
layout: post
title: Image Completion
date: '2022-08-19T10:00:00.000-03:00'
author: Andrés Herrera
tags: [Image Completion, Computer Vision]
author_id: andresh
category: [machine-learning]
featured_image: /images/image-completion/image-completion.png
permalink: /blog/image-completion-computer-vision/
---

In this blog, we will present the topic of image completion. With it, we'll show its use cases, the relevance of this topic, and how to solve it using deep learning models. There is also a link to a repository created by Xmartlabs to use a model specific for human face editing by applying inpainting strategies.

## What is image completion?

Image completion or Image inpainting is a research area in computer vision. Its main goal is to receive an incomplete image and output the prediction for what those unknown pixels should look like. It's considered a complex problem, primarily due to ambiguity when deciding on an acceptable prediction.

Image inpainting can be used in many cases, for example, restoring old damaged pictures or removing undesired objects or people in photos. Some online models allow you to input an image and mark which area to inpaint. See an example from a model available by NVIDIA ([link](https://www.nvidia.com/research/inpainting/)) below.

![Original Image.](/images/image-completion/index.png)
*Original Image.*

![Image with the region to modify.](/images/image-completion/img_w_mask.png)
*Image with the region to modify.*

![Prediction with the modified region.](/images/image-completion/original_result.png)
*Prediction with the modified region.*

The prediction done by the model is really convincing, especially considering the complex scenario where the model has to work. You would notice this image is not a "natural image" only by observing the region where the person used to be in great detail.

## How do image inpainting models work?

Being able to reconstruct an incomplete image is a challenging task, even for the best artists. Thanks to the improvement that deep learning has shown in the last years, we can now train a model to generate these reconstructions of partially seen scenarios. There are many ways to prepare these models, and researchers constantly present new creative methods.

This problem has been generally tackled by randomly occluding parts of images without any corruption and then trying to reconstruct those parts. The main advantage of posing the issue as self-supervised is that any dataset of images can be used to train our model, and no external labeling is needed! However, the model will not generalize well to other situations if the dataset only contains specific images (for example, only dog images).

Creating an image inpainting model can be separated into two parts:

1. Choosing the architecture to generate the image.
2. Having a reliable way to measure how good the prediction is.

The architecture for generating predictions tends to be some variation of the U-Net [1][2]. To solve the measurement of the generator's performance, a popular alternative is to add another discriminator model to obtain a Generative Adversarial Network (GAN).

A simple explanation for GANs is that two models are being trained simultaneously: the **generator** is trained to output real-looking images, and the **discriminator** decides whether that image is real or not. However, original GANs generated images from noise vectors. In this case, the network must also receive the image that needs inpaint to control what the output should look like. To achieve this, we can use conditional GANs (cGANs) [3]. For inpainting architectures, cGANs are very useful as they use the condition of the reference image and the noise vector to reconstruct. Another option for the training is using a known model such as the [VGG-16](https://medium.com/@mygreatlearning/everything-you-need-to-know-about-vgg16-7315defb5918) to measure perceptual loss. This method is used for training the NVIDIA model [1], which is well detailed in this [blog](https://towardsdatascience.com/pushing-the-limits-of-deep-image-inpainting-using-partial-convolutions-ed5520775ab4). For more information on deep learning applied to image inpainting, we suggest checking out **[10 Papers You Must Read for Deep Image Inpainting](https://towardsdatascience.com/10-papers-you-must-read-for-deep-image-inpainting-2e41c589ced0).**

Up to this point, the models we presented solve the problem of inpainting an incomplete image with the most suitable scenario according to the network. But note that we don't have any control over the output of those missing parts. In the example above, we may want to force the network to draw some plants in the rocks. **How can we add some expected output information to our model?**

## Image Completion use case: Deep Plastic Surgery

In a 2020 paper, the authors show that it's possible to reconstruct incomplete human faces just by following a sketch. The final product is a novel and robust image editing framework named Deep Plastic Surgery [4], which improves on previous models such as [SC-FEGAN](https://github.com/run-youngjoo/SC-FEGAN) [5] and [DeepFillv2](https://github.com/zhaoyuzhi/deepfillv2) [6]. You can use the Deep Plastic Surgery framework to generate human faces from sketches or edit a given face in a specific section with a reference sketch. The use case detailed next is face editing.

![Example of face editing.](/images/image-completion/teaser-d.png)
*Example of face editing.*

![teaser-f.png](/images/image-completion/teaser-f.png)

The images used to train this network come from the [CelebA-HQ dataset](https://research.nvidia.com/publication/2018-04_progressive-growing-gans-improved-quality-stability-and-variation), a higher-quality version of the [CelebA dataset](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html). Because this dataset doesn't provide a human-drawn sketch of the images, the authors of Deep Plastic Surgery use the Holistically-Nested Edge Detection (HED) [6] to extract edge maps and use them as the Sketch ground truth ($S_{gt}$). The dilation step restructures the edge maps into a rougher sketch, making it more similar to what a user would input to the network.

The framework's architecture is quite complex, with two generators and one discriminator. The first generator *G* inputs the mask (*M*), the ground truth image cropped where it must be completed ($I_{in}$), the dilated sketch ($S_l$), and the value used to control the dilation (*l*), there are two outputs, a new refined sketch ($S_{gen}$) and the first approximation of the inpainted image ($I_{gen}$). This generator is trained against the discriminator *D* to improve the sketch and image generated. Although the image $I_{gen}$ could be used as the final output, another fixed pre-trained model *F* is used to generate $I_{out}$ from the original cropped image, and the sketch generated by *G.* Testing the model shows that the output of the *F* generator is far superior to the output of the *G* model.

![Deep Plastic Surgery framework. The image is taken from [4].](/images/image-completion/Screenshot_from_2022-08-01_14-51-48.png)
*Deep Plastic Surgery framework. The image is taken from [4].*

The results from this model look very real in most cases. With the $l \in [0, 1]$ **hyper parameter, the user can tell the framework how truthful we should be towards the sketch; with $l = 1$ the model has more freedom.

The modifications available for human faces with the Deep Plastic Surgery model are multiple, from simulating a rhinoplasty to hair implants.

![Deep Plastic Surgery image editing examples of rejuvenation, hair implant, and chin surgery. The image is taken from [4].](/images/image-completion/Screenshot_from_2022-08-02_13-44-21.png)
*Deep Plastic Surgery image editing examples of rejuvenation, hair implant, and chin surgery. The image is taken from [4].*

To test the Deep Plastic Surgery framework with your own images, we provide a [repository](https://github.com/xmartlabs/FaceInpaintingDemo). It contains the original code for the models plus a notebook that converts the images into an accepted input. The input for the model is three images: the image to modify, the mask where the model should inpaint, and the sketch. We recommend [Photopea](https://www.photopea.com/) to generate the mentioned input.

## Conclusion

This area of computer vision is growing at a fast pace, primarily thanks to the creativity of those who make new research. Creativity is such an important part because, all in all, that's what the model is learning. Evaluating these models isn’t easy, as deciding what is acceptable isn’t straightforward. GAN architectures give a reasonable evaluation, although there is still room for improvement.

## References:

[1] Liu, G., Reda, F. A., Shih, K. J., Wang, T.-C., Tao, A., & Catanzaro, B. (2018). *Image Inpainting for Irregular Holes Using Partial Convolutions*. doi:10.48550/ARXIV.1804.07723

[2] Isola, P., Zhu, J.-Y., Zhou, T., & Efros, A. A. (2016). *Image-to-Image Translation with Conditional Adversarial Networks*. doi:10.48550/ARXIV.1611.07004

[3] Mirza, M., & Osindero, S. (2014). *Conditional Generative Adversarial Nets*. doi:10.48550/ARXIV.1411.1784

[4] Yang, S., Wang, Z., Liu, J., & Guo, Z. (2020). *Deep Plastic Surgery: Robust and Controllable Image Editing with Human-Drawn Sketches*. doi:10.48550/ARXIV.2001.02890

[5] Jo, Y., & Park, J. (2019). *SC-FEGAN: Face Editing Generative Adversarial Network with User’s Sketch and Color*. doi:10.48550/ARXIV.1902.06838

[6] Yu, J., Lin, Z., Yang, J., Shen, X., Lu, X., & Huang, T. S. (2019). Free-form image inpainting with gated convolution. *Proceedings of the IEEE International Conference on Computer Vision*, 4471–4480.

[7] Xie, S., & Tu, Z. (2015). *Holistically-Nested Edge Detection*. doi:10.48550/ARXIV.1504.06375
