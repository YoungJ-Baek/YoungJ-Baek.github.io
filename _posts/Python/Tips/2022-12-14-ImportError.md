---
title: "[Error/MacOS] ImportError: Library not loaded"
categories:
  - Python_Tips
tags:
  - Ubuntu
  - Linux
  - Error
toc: true
toc_sticky: true
comments: true
---

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

## 1. Preface

`ImportError` is very common error that programmers can face. Usually, it can be resolved via reinstalling the library or redirecting the path. However, in this case, it is related to MacOS. If you are facing the error in the certain environment below, you can try this solution.

- System
  - MacOS: Ventura 13.1
  - Python: 3.10.8
  - Pip: 22.2.2
  - Opencv-python: 4.6.0.66

## 2. Error

<div class="notice--primary" markdown="1">

`Error Log`

```
ImportError: dlopen(/opt/homebrew/lib/python3.10/site-packages/cv2/python-3.10/cv2.cpython-310-darwin.so, 0x0002): Library not loaded: /opt/homebrew/opt/ffmpeg/lib/libavcodec.59.dylib
  Referenced from: <9FC2913B-81A6-3EF6-8DC3-C221449C5803> /opt/homebrew/Cellar/opencv/4.6.0/lib/libopencv_videoio.4.6.0.dylib
  Reason: tried: '/opt/homebrew/opt/ffmpeg/lib/libavcodec.59.dylib' (no such file), '/System/Volumes/Preboot/Cryptexes/OS/opt/homebrew/opt/ffmpeg/lib/libavcodec.59.dylib' (no such file), '/opt/homebrew/opt/ffmpeg/lib/libavcodec.59.dylib' (no such file), '/usr/local/lib/libavcodec.59.dylib' (no such file), '/usr/lib/libavcodec.59.dylib' (no such file, not in dyld cache)
```

</div>

## 3. Solution

<div class="notice--primary" markdown="1">

`Command`

```bash
$ brew reinstall rav1e
```

</div>
