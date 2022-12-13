---
title: "[Error] E212: Can't open file for writing"
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

Sometimes, you should generate a file regarding the tutorial or documentation. However, many unexpected errors can interrupt you. One of them is `E212` error related to permission.

## 2. Error

<div class="notice--primary" markdown="1">

`Error Log`

```
E212: Can't open file for writing
Press ENTER or type command to continue:
```

</div>

## 3. Solution

### 3.1. Using sudo command

<div class="notice--primary" markdown="1">

`Command`

```bash
$ sudo vi {filename}
```

</div>

### 3.2. Give permission when save

<div class="notice--primary" markdown="1">

`Command`

```vim
:w !sudo tee %> /dev/null
```

</div>
