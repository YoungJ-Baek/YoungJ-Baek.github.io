---
title: "[Optical Flow/01] Coherence"
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

## Coherence

How do humans predict the movement of objects? Like many other areas of computer vision, optical flow has also evolved by analyzing the flow of human thought. As perceptive people may have already noticed, optical flow plays a significant role in predicting the movement of objects. So why is it called optical flow, instead of motion flow or object flow? Before answering this question, let's go back to the initial question.

> How do humans predict the movement of objects?

It can be based on observing muscle movement or experience. Upon further reflection, it can be understood that this is due to inertia. We expect stationary objects to remain stationary, and moving objects to continue in their direction. Therefore, in horror movies, the supernatural phenomenon that appears from different locations each time we blink can instill fear in viewers because it cannot be predicted.

As with other areas of computer vision, optical flow has drawn inspiration from the way humans perceive things. It establishes premises and seeks answers in situations where the premises are incomplete. This post will examine such premises.

## Two types of coherence

As mentioned earlier, all physical phenomena follow inertia, which can be expressed as consistency. In computer vision, our eyes will act as the camera and we will perceive the video as frames. There are two major consistencies in the video that are important and help us find solutions under unfavorable conditions.

### Image Coherence

When we look at a specific point in an image, there is a high probability that adjacent pixels also have similar values. Although the example may be a bit messy, if we look at the hand touching the mouse right now, we can find such consistency. Adjacent pixels of the skin color have a similar color. This consistency in the image is used in various fields, and the easiest field to encounter is Edge Detection. Areas where the difference between adjacent pixels is small are likely to be the same object, and areas where the difference is large are likely to be the boundary between objects. Figure 1 is a concept figure of image coherence.

<p align="center">
  <img src="/assets/images/posts/image_coherence.jpeg" alt>
  <em>Image Coherence</em>
</p>

### Time Coherence

When we view an image, objects move continuously. If the FPS (Frame Per Second) is sufficiently high, then objects that can teleport or change direction without delay in 180 degrees can be a counterexample to this post. If you have such examples, please leave a rebuttal comment with a reference URL, and I would appreciate it (you may even see the author in the news soon).

In other words, for a large change to occur, small changes must precede it. This means that if the pixel value at time t is $f(y,x,t)$, then $f(y, x, t+1)$ is likely to be the same or very similar. If the values are the same, it can be inferred that there was no movement. By utilizing this feature, basic segmentation can be performed. The difference between two images can be used to extract only the objects with large changes. This temporal consistency becomes a very important clue in Optical Flow. Figure 2 is a concept figure of time coherence.

<p align="center">
  <img src="/assets/images/posts/time_coherence.jpeg" alt>
  <em>Time Coherence</em>
</p>

## Conclusion

In this post, we have discovered clues for calculating optical flow from a computer vision perspective. However, the most important thing is missing. So, what is Optical Flow? It's a natural question that should come to mind. Intentionally, the definition of Optical Flow is not mentioned in this chapter. It may have been perceived as "something to calculate the motion of objects." But is it possible for a computer to calculate the motion of objects like humans do? In the next chapter, we will cover what Optical Flow is. Is it really about calculating the motion of objects?

## Reference
