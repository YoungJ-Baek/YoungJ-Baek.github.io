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
This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek "@embed")
{: .notice--info}

## 1. Goal
The goal of this post is to develop test code for loop closing of LDSO. We decided it to check the feasibility of localization and loop closing of our application. You can see more details about our meeting minutes in [here](https://v-slammers.github.io/minutes_arnavi/meeting-minutes/). We already have prepared pre-generated PCL map, DBoW, and pose binary files. To see how to generate those things, look at this [post]() (TBD). We divide this process into 7 steps. Let's take a look for each steps.

## 2. Argument
To trigger loop closing, we need 4 things. We set these four parameters as arguments. You can find more details as followed. Listing order is same with argument order.

1. Source: Input image
2. Calibration: Predefined value for calibration
3. Vocabulary: In our test code, we use ORB vocabulary
4. DBoW: Database of bag-of-words

## 3. Test Code
### 3.1. Load ORB Vocabulary
In KITTI example of LDSO, we can find vocabulary loader part. LDSO uses ORB vocabulary, so we will use it as well.

<div class="notice--primary" markdown="1">

`Load ORB Vocabulary`
```cpp
    shared_ptr<ORBVocabulary> orb3_vocabulary(new ORBVocabulary());
    orb3_vocabulary->load(argv[3]);
    std::cout << "vocabulary loaded\n";
```

</div>

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

<div class="notice--primary" markdown="1">

`Load Input Image`
```cpp
    shared_ptr<ImageFolderReader> reader(new ImageFolderReader(ImageFolderReader::KITTI, argv[1], argv[2],"",""));
    reader->setGlobalCalibration()
    shared_ptr<ImageAndExposure> img(reader->getImage(0));
    std::cout << "reader set done\n";
```

</div>

### 3.4. Convert Image to Frame
Then, our next step is to make frames including multiple pyramids via conversion from the input image. In LDSO, this function is implemented at `addActiveFrame` in `FullSystem`. During the conversion, two Hessian are generated, `Frame Hessian` and `Calibration Hessian`. Note that all the camera intrinsic parameters were initialized at `setGlobalCalibration` function.

<div class="notice--primary" markdown="1">

`Convert Image to Frame`
```cpp
    // Create Calibration Hessian
    shared_ptr<Camera> camera(new Camera(fxG[0], fyG[0], cxG[0], cyG[0]));
    camera->CreateCH(camera)

    // Create Frame Hessian
    shared_ptr<Frame> frame(new Frame(img->timestamp));
    frame->CreateFH(frame);
    shared_ptr<FrameHessian> frame_hessian = frame->frameHessian;

    // Convert Image to Frame with Generating Image Pyramids
    frame_hessian->ab_exposure = img->exposure_time;
    frame_hessian->makeImages(img->image, camera->mpCH);
    std::cout << "frame created\n";
```

</div>

### 3.5. Calculate BoW via Feature Detection
In LDSO, there are two ways to select pixels. Following `PixelSelector`, both corners and non-corners are selected to decide whether the frame is key frame or not. On the other hand, corners are picked to calculate bag-of-words of each key frames. So, calculation of bag-of-words can be described with two parts, corner detection and bag-of-words calculation.

<div class="notice--primary" markdown="1">

`Calculate BoW`
```cpp
    // Corner Detection
    FeatureDetector detector;
    frame->features.reserve(setting_desiredImmatureDensity);
    detector.DetectCorners(setting_desiredImmatureDensity, frame);
	
    // BoW Calculation
    for(auto &feature: frame_hessian->frame->features){
        feature->ip = shared_ptr<ImmaturePoint>(new ImmaturePoint(frame_hessian->frame, feature, 1, camera->mpCH));
    }
    frame->ComputeBoW(orb3_vocabulary);
```

</div>

As a result, `bowVec` of `frame` structure is updated with calculated bag-of-words. Also, `featVec` of the structure is updated with new features.

### 3.6. Detect Loop Closing via BoW
In DBoW3, there is a function, `query`. We will use this function to detect loop closing using BoW.

<div class="notice--primary" markdown="1">

`Detecting Loop Closing via BoW`
```cpp
    keyframe_database->query(frame->bowVec, results, 1);

if(results.empty()){
    std::cout << "no loop found\n";
    exit(1);
}
DBoW3::Result r = results[0];
std::cout << r.Id << "\n";
```

</div>

### 3.7. Correction
(TBD)

## 4. Experiment
(TBD)

## 5. Conclusion
(TBD)