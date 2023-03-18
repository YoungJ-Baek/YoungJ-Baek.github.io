---
title: "[Optical Flow/08] Optical Flow Dataset"
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

As deep learning-based optical flow algorithms have emerged, datasets have become a very important keyword. Optical flow is difficult to obtain ground truth for, and even if ground truth is obtained in the real world, the amount of data is very limited. In other computer vision fields such as object detection, data labeling is easy, making it relatively easy to solve these problems. However, the optical flow field still lacks in both quantity and quality.

Nevertheless, as always, humans have found solutions, and a revolutionary method has emerged in the optical flow field, which has become the industry standard. In the field of Optical Flow, there are mainly four types of datasets that are commonly used:

- Flying Chairs
- Flying Things 3D
- MPI-Sintel
- KITTI

To briefly introduce, Flying Chairs/Flying Things 3D are graphic (synthetic) datasets. Therefore, the input values become the labels and ground truth of Optical Flow. Despite being an artificial dataset, it is widely used and has become a standard for training, thanks to the ease of labeling.

On the other hand, MPI-Sintel/KITTI are real datasets. However, due to the nature of Optical Flow, it is difficult to obtain a large amount of ground truth data, so only a small amount of data is provided. Therefore, it is used for fine-tuning and testing.

To summarize the above explanations, the training and testing process of an Optical Flow model is as follows:

- Training (scheduling): Flying Chairs/Flying Things 3D
- Training (fine-tuning before test): Flying Things 3D/MPI-Sintel/KITTI
- Testing: MPI-Sintel/KITTI

## Flying Chairs/Flying Things 3D

The details about those datasets will be introduced in next chapters, FlowNet and FlowNet 2.0. So, we will talk about the details later. Now, here is download links as follows:

- [Flying Chairs](https://lmb.informatik.uni-freiburg.de/resources/datasets/FlyingChairs.en.html#flyingchairs)
- [Flying Things 3D](https://lmb.informatik.uni-freiburg.de/resources/datasets/SceneFlowDatasets.en.html)

## MPI-Sintel

MPI (Max Planck Institute) Sintel is a dataset extracted from the 3D short animation "Sintel". It consists of a total of 1064 images, and the site introduces the features of the dataset as follows:

- Very long Sequences
- Large Motions
- Specular Reflections
- Motion Blur
- Defocus Blur
- Atmospheric Effects

The official site and download link are as follows:

- [Official site](http://sintel.is.tue.mpg.de/)
- [MPI-Sintel](http://sintel.is.tue.mpg.de/downloads)

## Reference
