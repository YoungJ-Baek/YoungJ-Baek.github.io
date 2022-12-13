---
title: "[Error] Error while loading shared libraries"
categories:
  - CS_Linux
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

There are two types of library, static and dynamic. Sometimes, you may face an error related to shared libraries even though you have built it well. It's because you have compiled and built it well, but it has been built in the user path, `/usr/local/lib`

## 2. Error

The error log below is an example of my case, `libpango_windowing.so` problem.

<div class="notice--primary" markdown="1">

`Error Log`

```
error while loading shared libraries: libpango_windowing.so: cannot open shared object file: No such file or directory
```

</div>

## 3. Solution

### 3.1. make configuration file

<div class="notice--primary" markdown="1">

`Command`

```bash
$ cd /etc/ld.so.conf.d/
$ sudo vi libpango_windowing.conf
```

You can replace `libpango_windowing.conf` with your problematic shared library in form of `lib{xxxxxx}.conf`. Then, type the line below in the configuration file.

`lib{xxxxx}.conf`

```vim
/usr/local/lib
```

Then, type the command below after saving the configuration file

`Command`

```bash
$ sudo /sbin/ldconfig
```

</div>

### 3.2. Add Library Path

<div class="notice--primary" markdown="1">

Add library path in the prompt or profile.

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:{library path}
```

</div>
