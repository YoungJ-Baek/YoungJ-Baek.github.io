---
title: "[Rust] Hello World"
categories:
  - Rust_Article
tags:
  - Rust
toc: true
toc_sticky: true
comments: true
---

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

This post is written referring to the [official documentation](https://doc.rust-lang.org/book/title-page.html)
{: .notice--warning}

This post is based on `M1 Macbook Pro 14 inch`, macOS Ventura 13.0
{: .notice--warning}

## 1. Preface

Printing `Hello, world!` is usually very first step of learning programming language. So, today, I will introduce how to print our bible.

## 2. Print Hello World

### 2.1. Prepare Project Folder

First, open your terminal, and then type the command below to make project folder. We will use this folder many time during learning `Rust`, so I recommend to make it this time.

<div class="notice--primary" markdown="1">

`Command`

```bash
$ mkdir projects
$ cd projects
$ mkdir hello_world
$ cd hello_world
```

</div>

### 2.2. Create Main file

Second, create main file in the directory. If you have learned `C/C++` or `Python` before, it is same with `main.c/main.cpp` or `main.py`. `Rust` uses `.rs` as an extention. After you have generated the file, type the code below.

<div class="notice--primary" markdown="1">

`main.rs`

```rs
fn main() {
    println!("Hello, world!");
}
```

</div>

Now, you are ready to print `Hello, world`.

### 2.3. Compile and Run

Third, you are now ready to compile the file and run it. In `C/C++`, you can do this via `make` command. In `Rust`, you can do this with `rustc` command instead.

<div class="notice--primary" markdown="1">

`Compile and Run`

```bash
$ rustc main.rs
$ ./main
```

`Result`

```bash
Hello, world!
```

</div>

## 3. Deep Dive

Now, you have printed `Hello, world` with `Rust`. You can find some differences compared to other languages, especially `C++`.

1. `Rust` uses `4 spaces` instead of `tab` to indent
2. `println!` calls `Rust macro`. If you want to call a function named `println`, call it without `!`. More details about it will be described later
3. Like `C++`, we use `;` to end a line

Moreover, we have learned `rustc` works like `make` in `C/C++`. So, we can compile and run the file using this command. However, if you can remember the cons of `make` command, I am sure that you wish there may be a command like `cmake` to compile multiple files or entire project. Fortunately, `Rust` has that option. I will introduce it at the very next post.
