---
title: "[Rust] Install Rust"
categories:
    - Blog_Tips
tags:
    - Git
toc : true
toc_sticky: true
comments: true
---
This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

This post is written referring to the [official documentation](https://doc.rust-lang.org/book/title-page.html)
{: .notice--warning}

## 1. Preface
Today, I will introduce how to install `Rust` in your Macbook. Recently, I have been interested in `Rust`, so I install it in my M1 Macbook Pro 14`. This post covers only how to install it with MacOS. Therefore, if you want to install it with Windows or Linux, please refer the official document at the top of this post.


## 2. Installation
### 2.1. Install rustup tool
First, open your terminal, and then type the command below. It will install `rustup` tool, which installs the latest stable version of `Rust`.

<div class="notice--primary" markdown="1">

`Command`
```bash
$ curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh
```

</div>

After typing the command, you can select three options, 1) Proceed with installation (default), 2) Customize installation, 3) Cancel installation. I select the first one, but if you want other setting, follow the guide of the official document.

Then, you can see the message that you have successed the installation, `Rust is installed now. Great!`.

<div class="notice--danger" markdown="1">

If you face linker errors, you should install a C compiler. For MacOs, you can install it with following command.
```bash
$ xcode-select --install
```

</div>


### 2.2. Add Path
Second, reload the terminal to add the path where `Rust` is installed to your `PATH`. If you do not want to reload it, you should add it manually.

<div class="notice--primary" markdown="1">

`Add PATH manually`
```bash
$ source $HOME/.cargo/env
```

</div>

Then, check the version of `Rust` to see whether it has been installed well. In my case, I can see the message as followed.

<div class="notice--primary" markdown="1">

`Add PATH manually`
```bash
youngjin@youngjinui-MacBookPro ~ % rustc --version
rustc 1.64.0 (a55dd71d5 2022-09-19)
```

</div>


### 2.3. Update and Uninstall
Third, if you want to update your `Rust` to the latest version, type the first command below. Otherwise, if you want to uninstall, use the second one.

<div class="notice--primary" markdown="1">

`Update Rust`
```bash
$ rustup update
```

`Uninstall Rust`
```bash
$ rustup self uninstall
```

</div>


### 2.4. Troubleshooting
This is the end of `Rust` installation. If you have faced any problem, you'd better to find the official document, especially [installation part](https://doc.rust-lang.org/book/ch01-01-installation.html).