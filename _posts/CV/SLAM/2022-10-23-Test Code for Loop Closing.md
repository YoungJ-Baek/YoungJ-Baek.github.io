---
title: "[LDSO] Test Code for Loop Closing"
categories:
    - CV_SLAM
tags:
    - LDSO
    - DSO
    - Loop Closing
toc : true
toc_sticky: true
comments: true
---
This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

## 1. Goal
The goal of this post is to develop test code for loop closing of LDSO. So, we prepare pre-generated PCL map, DBoW, and pose binary files. To see how to generate those things, look at this [post]() (TBD). We divide this process into 7 steps. Let's take a look for each steps.

## 2. Argument
To trigger loop closing, we need 4 things. We set these four parameters as arguments. You can find more details as followed. Listing order is same with argument order.

1. Source: Input image
2. Calibration: Predefined value for calibration
3. Vocabulary: In our test code, we use ORB vocabulary
4. DBoW: Database of bag-of-words

## 3. Test Code
### 3.1. Load ORB Vocabulary
In KITTI example of LDSO, we can find vocabulary loader part. LDSO uses ORB vocabulary, so we will use it as well.

```cpp
    // Load Vocabulary
	shared_ptr<ORBVocabulary> orb3_vocabulary(new ORBVocabulary());
	orb3_vocabulary->load(argv[3]);
	std::cout << "vocabulary loaded\n";
```

### 3.2. Load DBoW Database
### 3.3. Load Input Image
1. should be non key frame close to the loop
2. should use Image Folder Loader
### 3.4. Convert Image to Frame
### 3.5. Select Feature (Pixel Selection)
### 3.6. Detect Loop Closing via BoW
first goal
### 3.7. Correction
if needed