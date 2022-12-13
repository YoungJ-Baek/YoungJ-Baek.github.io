---
title: "[Ubuntu] Install Notepad++"
categories:
  - Blog_Tips
tags:
  - Ubuntu
  - Linux
  - Notepad
toc: true
toc_sticky: true
comments: true
---

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

## 1. Preface

**Notepad++** is very useful tool for Ubuntu users for a basic editor. This post describes how to install it based on `Ubuntu 20.04`.

## 2. Installation

### 2.1. Install snap

First, open your terminal, and then type the command below. It will install `snap` tool, prerequiries for notepad.

<div class="notice--primary" markdown="1">

`Command`

```bash
$ sudo apt install snapd snapd-xdg-open
```

</div>

### 2.2. Install Notepad++

Second, install **Notepad++** using `snap`.

<div class="notice--primary" markdown="1">

`Command`

```bash
$ sudo snap install notepad-plus-plus
```

</div>

## 3. Run

### 3.1. Run Notepad++

<div class="notice--primary" markdown="1">

`Command`

```bash
$ notepad-plus-plus
```

</div>

### 3.2. Open txt file

<div class="notice--primary" markdown="1">

`Command`

```bash
$ notepad-plus-plus {file.txt}
```

</div>
