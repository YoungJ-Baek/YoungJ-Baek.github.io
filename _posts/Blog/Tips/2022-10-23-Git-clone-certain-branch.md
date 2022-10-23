---
title: "[Git] Cloning certain branch"
categories:
    - Blog
tags:
    - Git
toc : true
toc_sticky: true
comments: true
---
This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}
You can find more posts about `Git` easily by searching the `Git` tag.
{: .notice--warning}

## 1. Preface
Sometimes, you may want to clone certain branch of the repository. If other team or branch implement some good functions, it would be better to clone it rather than the master branch. In my case, [our team](https://github.com/V-SLAMMERS/) usually collaborate by dividing into two parts, and sometimes I want to start my branch with other part's. In this post, you can figure out how to clone the certain branch, not the master.

## 2. Cloning Certain Branch
<div class="notice--primary" markdown="1">
`Command`
```bash
git clone -b {branch name} --single-branch {repository URL}
```
`Example`
```bash
git clone -b jm --single-branch https://github.com/V-SLAMMERS/LDSO
```
</div>
In this case, you can clone `jm` branch of `LDSO` repository of `V-SLAMMERS`.
