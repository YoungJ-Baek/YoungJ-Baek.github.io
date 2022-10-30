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
After loading ORB vocabulary, we need to load pre-generated DBoW database. It was resulted from map generation. So, it has all the information about bag-of-words of map. In LDSO, bag-of-words of key frames is added to database at loop closing thread. However, since we already have pre-generated database, we don't need addition. Instead, all we need to do is load the database and detect loop closing via bag-of-words. In this chapter, the post describes how to load database.

Also, you can find bag-of-words structure in `Frame` data structure in LDSO. In this structure, there's a function named `ComputeBoW` to compute bag-of-words of a single frame. So, we have to initialize this structure as well.

<div class="notice--primary" markdown="1">
`ComputeBoW`
```cpp
void Frame::ComputeBoW(shared_ptr<ORBVocabulary> voc) {
    // convert corners into BoW
    vector<cv::Mat> allDesp;
    for (size_t i = 0; i < features.size(); i++) {
        auto &feat = features[i];
        if (feat->isCorner) {
            cv::Mat m(1, 32, CV_8U);
            for (int k = 0; k < 32; k++)
                m.data[k] = feat->descriptor[k];
            allDesp.push_back(m);
            bowIdx.push_back(i);
        }
    }
    voc->transform(allDesp, bowVec, featVec, 4);
}
```
`Load DBoW Database`
```cpp
    // Load DboW database
    DBoW3::Database database_bow;
    database_bow.load(argv[4]);
    std::cout << "database loaded\n";
    
    // Initialize Query for Loop Closing Candidate
    DBoW3::QueryResults results;
    DBoW3::Result result;

    // Initialize BoW Structure for Input Frame
    DBoW3::BowVecture frame_bow;
    DBoW3::FeatureVector frame_feature;
```
</div>

### 3.3. Load Input Image
Next, we should load an input image to detect loop closing. Easily, we can load an image with OpenCV or using other methods. However, in LDSO, we should load an image with `ImageFolderLoader`. Also, there is one more condition to detect loop closing. We should pick a non key frame which is close to the loop. Note that we use `ImageAndExposure` class for single frame. More details about image loader is on this [post](). (TBD)

```cpp
// Load Input Image
shared_ptr<ImageFolderReader> reader(new ImageFolderReader(ImageFolderReader::KITTI, argv[1], argv[2],"",""));
reader->setGlobalCalibration()
shared_ptr<ImageAndExposure> img(reader->getImage(0));
std::cout << "reader set done\n";
```

### 3.4. Convert Image to Frame

### 3.5. Select Feature (Pixel Selection)

### 3.6. Detect Loop Closing via BoW
first goal

### 3.7. Correction
if needed