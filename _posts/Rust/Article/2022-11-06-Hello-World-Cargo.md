---
title: "[Rust] Hello World with Cargo"
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

We already printed `Hello, world` with `rustc` command to compile and run in last post. However, there is another way to compile and run, `cargo`. The relationship between `rustc` and `cargo` is similar to `make` and `cmake` in `C/C++`.

## 2. Print Hello World with Cargo

### 2.1. Prepare Project Folder

First, go back to your `projects` directory, and then type the command below to make other folder for `cargo`.

<div class="notice--primary" markdown="1">

`Command`

```bash
$ cargo new hello_cargo --bin
$ cd hello_cargo
```

</div>

First line means you will create a new project named `hello_cargo`, not a library but a binary purpose. Then, there will be two files and one directory, `Cargo.toml`, and `src` directory including `main.rs` file in it.

### 2.2. Cargo.toml

If you generate `Rust` project with `cargo`, you will manage it with `Cargo.toml` file. In this file, you can put all the information of the project including name, version, and authors. Moreover, you can manage all the dependencies of the project in this file. For now, there is no dependency, but we will add something at the next post.

<div class="notice--primary" markdown="1">

`Cargo.toml`

```yaml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"
authors = ["YoungJin-Baek <qordudwls1@gmail.com>"]

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]

```

</div>

By the way, `cargo` already generate main file with some example code to print `Hello, world`. So, you do not have to add anything for it. Now, you are ready to print `Hello, world` with `cargo`.

### 2.3. Compile and Run (1)

Third, you are now ready to compile the file and run it. `Cargo` compiles and runs the files under `src` directory. So, all you have to do for compile and run is to add files under the `src` directory. You do not have to learn other things unlike `cmake`.

<div class="notice--primary" markdown="1">

`Compile and Run`

```bash
$ cargo build
   Compiling hello_cargo v0.1.0 (/Users/youngjin/Desktop/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.62s
```

`Run`

```bash
$ ./target/debug/hello_cargo
```

`Result`

```bash
Hello, world!
```

</div>

Note that compiled file is located at `target/debug/`.

### 2.4. Compile and Run (2)

`Cargo` provides another way to compile and run the project. You do not have to compile and run seperately, but you can do both of them spontaneously. All you have to do is typing simple command.

<div class="notice--primary" markdown="1">

`Compile and Run`

```bash
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/hello_cargo`
```

`Result`

```bash
Hello, world!
```

</div>

In this example, there is no log related to compiling. It is because we have already compile the project before, and there is no change after that. So, `cargo` do not have to build the project again, instead, it runs the file.

### 2.5. Cargo Check

`Cargo` provides very interesting function. It checks whether the project is able to be compiled or not. So, if you want to check there is no error, you can use this command. Also, it does not generate binary file for the result, it saves the time via not generating the file.

<div class="notice--primary" markdown="1">

`Cargo Check`

```bash
$ cargo check
    Checking hello_cargo v0.1.0 (/Users/youngjin/Desktop/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33s
```

</div>

### 2.6. Build for Release

You can make release version via `cargo`, too. It is very simple, but takes longer time compared to building for debug. So, when you are ready to release your project, use the command below. Otherwise, use the command in chapter 2.3 or 2.4.

<div class="notice--primary" markdown="1">

`Build for Release`

```bash
$ cargo build --release
   Compiling hello_cargo v0.1.0 (/Users/youngjin/Desktop/projects/hello_cargo)
    Finished release [optimized] target(s) in 2.29s
```

</div>

Unlike building for debug, the result file will be generated in `target/release` directory. You can run this file when you need to benchmark your software. Everything will have been optimized via `cargo`.
