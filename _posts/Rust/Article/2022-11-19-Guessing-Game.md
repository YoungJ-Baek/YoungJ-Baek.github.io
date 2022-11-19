---
title: "[Rust] Guessing Game using Rand"
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

This post is written referring to the [official documentation](https://doc.rust-lang.org/book/title-page.html), [Programming a Guessing Game](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html)
{: .notice--warning}

This post is based on `M1 Macbook Pro 14 inch`, macOS Ventura 13.0
{: .notice--warning}

## 1. Preface

Now, we are able to use `cargo` to make new project and manage it. Usually, many programming languages suggest basic syntax and grammer for beginners. However, the official documentation of `Rust` suggests programming a guessing game, a simple program for beginners. In my opinion, it is very attractive and fancy approach for the later programming language. In this post, I will follow the official guidance and record my trials-and-errors to help others.

## 2. Setting up a new project

### 2.1. Prepare New Project with Cargo

First, go back to your `projects` directory, and then type the command below to make other folder for `cargo`.

<div class="notice--primary" markdown="1">

`Command`

```bash
$ cargo new guessing_game
$ cd guessing_game
```

</div>

First line means you will create a new project named `guessing_game`, not a library but a binary purpose. Then, there will be two files and one directory, `Cargo.toml`, and `src` directory including `main.rs` file in it.

### 2.2. Cargo.toml

If you generate `Rust` project with `cargo`, you will manage it with `Cargo.toml` file. In this file, you can put all the information of the project including name, version, and authors. Moreover, you can manage all the dependencies of the project in this file.

<div class="notice--primary" markdown="1">

`Cargo.toml`

```yaml
[package]
name = "guessing_game"
version = "0.1.0"
edition = "2021"
authors = ["YoungJin-Baek <qordudwls1@gmail.com>"]

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
rand = "0.8.5"
```

</div>

## 3. Code

The code for guessing game is composed of three parts, to get user input, to generate random number, and to compare two of them. Here is the entire code for it, and more details about the code will be described in chapter 4.

<div class="notice--primary" markdown="1">

`main.rs`

```rs
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    loop {
        println!("Please input your guess.");

        // let apple = 5 // immutable
        let mut guess = String::new(); // mutable

        io::stdin()
            .read_line(&mut guess) // it is important to add &mut to modify references; if you use &guess, it is immutable
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {guess}");

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

</div>

## 4. Details

### 4.1. Get User Input

To obtain user input, we need to call input/output library, `io`. It is very similar to the `iostream` in `C++`. We can know that the library is in the standard library, `std`.

I wonder that the standard library is similar to the namespace `std` in `C++`. However, I have not searched it for sure, so it is just my opinion now.
{: .notice--danger}

Next, we create a variable named `guess` via using `let` statement. In this point, we should take a look at `mut` syntax. In `Rust`, all the variables are immutable by default setting. It is very different from other languages like `C++`. In `C++`, we should add `const` to make a variable immutable. When you develop a large program, it is very inconvenient that add `const` to all variables that should not be modified.

`io::stdin()` is standard input library. In the library, you can find `read_line()` function. It takes whatever the user types and convert it into a string. So, we need to use string as an argument. Also, it should be mutable so that the method can modify the value. Moreover, the function requires `&` syntax as an argument. It is very similar to `C++`'s reference syntax. However, more details about it will be described later.

### 4.2. Generate Random Number

To generate random number, we add `use rand::Rng;` syntax. Remember that we have already add `rand` crate in our `Cargo.toml`. Now, we can use all the functions in `rand` crate. So, we call `thread_rng()` to generate random number. `get_range(start..=end)` decides the random number generating rule, generating via lower and upper range. So, now we can generate a random number in the range of 1 ~ 100.

### 4.3. Compare 2 Numbers

To compare two numbers, we should add `use std::cmp::Ordering;` syntax. `Ordering` function compares two numbers and returns the status of the result, `Less`, `Greater`, and `Equal`. If we use `C++` or other languages, we should use `if` statement to print different answers depending on the conditions. Instead, we can use `match` statement to define the operations depending on the return value. More details about `match` will be posted later.

## 5. Note

In the code, there are two variables named `guess`. In most of programming language, it is abandoned to use define multiple variables with same name. However, `Rust` says it is okay. It is very interesting point, and we will talk about it later in a deep dive.

Also, `mut` and `reference` are very interesting, too. Especially, `mut` is something very new to me. We will talk about it at the very next post.
