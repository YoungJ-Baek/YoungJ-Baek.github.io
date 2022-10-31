---
title: "[Git page] Modify the font size of Git page"
categories:
    - Blog_Tips
tags:
    - Git
    - Git page
toc : true
toc_sticky: true
comments: true
---
This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

You can find more posts about `Git/Git page` easily by searching the `Git/Git page` tag.
{: .notice--warning}

## 1. Preface
This post is based on the `minimal-mistakes` theme. You can find more details about the theme in [here](https://mmistakes.github.io/minimal-mistakes/).

## 2. Modify the Font Size
To modify the font size, all you have to do is to modify single `scss` file, `_reset.scss`. The directory and how to modify are as followed.

<div class="notice--primary" markdown="1">
`Directory`
```bash
YOUNGJ-BAEK.GITHUB.IO/_sass/_reset.scss
```
`How to modify`
```html
// To change the font size, you need to modify font-size parameters in line 7 ~ 27
html {
  /* apply a natural box layout model to all elements */
  box-sizing: border-box;
  background-color: $background-color;
  font-size: 16px;

  @include breakpoint($medium) {
    font-size: 16px;
  } // default: 18px

  @include breakpoint($large) {
    font-size: 16px;
  } // default: 20px

  @include breakpoint($x-large) {
    font-size: 16px;
  } // default: 22px

  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}
```
</div>
