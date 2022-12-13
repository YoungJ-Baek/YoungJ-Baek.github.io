---
title: "[make] Compile with multi-core"
categories:
  - Cpp_Tips
tags:
  - Cpp
  - make
toc: true
toc_sticky: true
comments: true
---

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

## 1. Preface

In many C++ projects, compile and build are very hard task for programmers. Since the projects are so big, it usually takes long time to compile them. Fortunately, CPU has been improved through last few years. So, it would be better to use multi-core for compiling and building to reduce time cost.

## 2. Command

<div class="notice--primary" markdown="1">

`Command`

```bash
$ make -j{number of cores}
```

</div>
