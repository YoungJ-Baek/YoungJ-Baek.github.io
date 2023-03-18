---
title: "[Optical Flow/02] Motion Field vs Optical Flow"
categories:
  - CV_Optical_Flow
tags:
  - Optical Flow
  - Computer Vision
  - Image Signal Processing
toc: true
toc_sticky: true
comments: true
---

<div class="notice--info" markdown="1">

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)

You can see the original Korean version at [Searching Fundamental](https://searching-fundamental.tistory.com/category/Computer%20Vision/Optical%20Flow)

</div>

## Preface

In the previous post, we found clues for calculating Optical Flow from a computer vision perspective. More precisely, we found clues to enable a computer to perceive the motion of an object like a human does. But does this mean that calculating Optical Flow is all that is left? Can a computer truly perceive the motion of objects like humans do?

In this post, we will compare Motion Field and Optical Flow, which is named after the motion of objects. Surprisingly, Optical Flow does not represent the motion of objects. So, what exactly is it? Let's first take a look at Motion Field, which represents the motion of objects.

## Motion Field

Our friendly neighbor Wikipedia defines Motion Field as follows:

> In computer vision the motion field is an ideal representation of 3D motion as it is projected onto a camera image.(...) The motion field is an ideal description of the projected 3D motion in the sense that it can be formally defined but in practice it is normally only possible to determine an approximation of the motion field from the image data.

In short, Motion Field is an ideal representation of 3D motion as it is projected onto a camera image in computer vision. It captures all the movements of objects. The following figure shows an ideal Motion Field.

<p align="center">
  <img src="/assets/images/posts/ideal_motion_field.png" width="100%" height="100%" alt>
  <em>Ideal Motion Field [Reference: Bahadir K. Gunturk, EE Image Analysis II]</em>
</p>

The terms "ideal" and "in practice" in the definition of the Motion Field on Wikipedia suggest that it is an idealized representation of 3D motion projected onto a camera image, and that while it can be formally defined, in practice it is often only possible to determine an approximation of the motion field from image data. In other words, it is impossible to accurately reproduce the motion field from 2D images or videos that we commonly encounter, unless using a holographic 3D point cloud.

<p align="center">
  <img src="/assets/images/posts/ideal_motion_field.png" width="100%" height="100%" alt>
  <em>comparison between ideal Motion Field(right) and Projected 3D Motion in real world(left)</em>
</p>

There are several reasons for this, but to put it simply, it is because of the difference in dimensions as shown in the figure 4. Actual motion occurs in 3D space. However, the images or videos that we need to obtain a motion field from are 2D data. As the dimensions are reduced, numerous vectors in 3D space are projected onto 2D space, causing overlapping as shown in the figure. As a result, a significant amount of information is lost and distortion occurs. It is already difficult to capture things as they are, and attempting to capture all motion is ambitious.

<p align="center">
  <img src="/assets/images/posts/motion_field_vs_optical_flow.png" width="100%" height="100%" alt>
  <em>Motion Field vs Optical Flow [Reference: Franz, 2005; a) Motion of the sphere without grey value changing; b) Motion of the light source with grey value changing]</em>
</p>

Due to this information loss, we cannot accurately obtain the Motion Field in real-world images. The most representative example is errors that occur in the rotation of objects and light sources, as seen in the above image. The image on the left shows an example where actual motion (rotation) occurred, but there appears to be no change in the image. Conversely, the image on the right shows an example where there was actually no motion, but changes in brightness occurred due to the movement of the light source, making it appear as if there was a change in the image. In other words, the problem arises when there is actual movement but no motion vector occurs (FN) or when there is no actual movement but a motion vector occurs (FP). Through this example, we can understand what Optical Flow is. Optical Flow is not strictly speaking a method for capturing the movement of objects. So what is it?

## Optical Flow

Again, Our friendly neighbor Wikipedia defines Optical Flow as follows:

> Optical Flow or optic flow is the pattern of apparent motion of objects, surfaces, and edges in a visual scene caused by the relative motion between an observer and a scene.

Actually, this sentence is not easy to understand. To express it accurately, it is not easy to know what the differences are compared to the Motion Field. The reason is that this definition lacks the "How". Conceptually, it is a major cause of confusion because there is little difference between it and the Motion Field. Therefore, I prefers the second definition explained by Wikipedia, which includes the "How".

> Optical Flow can also be defined as the distribution of apparent velocities of movement of brightness pattern in an image.

Optical Flow is the process of capturing changes in image frames by considering only brightness patterns, or changes in luminance. In an image, luminance changes lead to variations in pixel values, and by analyzing the difference between the previous and current frames and the relationship between the current pixel value and its surrounding pixels, the motion of each pixel can be approximated. Optical Flow does not explicitly calculate motion, but by computing changes in luminance caused by motion, it implicitly generates a map that can serve as a Motion Field.
The reason for separating Optical Flow from Motion Field is that Motion Field is not an accurate concept and can limit the scope of calculating motion. Optical Flow, which generates a Flow Map based only on changes in luminance, is an independent estimation method that does not attempt to detect objects or reflect their motion. This aspect is what sparked the strong interest of me, who specializes in signal processing.

## Conclusion

In this post, we have looked at the concept of Optical Flow. In the next post, we will examine what conditions are necessary to actually calculate Optical Flow. As a hint, the concept of Coherence that we discussed in the previous post also appears here in the same way, except the terms are changed to Spatial Coherence and Temporal Persistence.

## Reference

1. [Motion Field - Wikipedia](https://en.wikipedia.org/wiki/Motion_field)
2. [Optical Flow - Wikipedia](https://en.wikipedia.org/wiki/Optical_flow)
