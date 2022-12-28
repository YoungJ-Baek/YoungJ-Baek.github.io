---
title: "[MacOS] Set C++ environment with Visual Studio Code"
categories:
  - Cpp_Tips
tags:
  - Cpp
  - VScode
  - MacOS
toc: true
toc_sticky: true
comments: true
---

This post is written by [YoungJ-Baek](https://github.com/YoungJ-Baek)
{: .notice--info}

## 1. Preface

This post describes how to set C++ environment at MacOS via Visual Studio Code. The post is assuming that VSCode and Homebrew are already installed.

## 2. Clang

MacOS uses Clang as a compiler. So, you need to check whether it is installed or not. If it is not installed, you need to install it.

<div class="notice--primary" markdown="1">

`Check Clang is installed`

```bash
$ clang --version
Apple clang version 14.0.0 (clang-1400.0.29.202)
Target: arm64-apple-darwin22.2.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

`Install if it not installed`

```bash
$ xcode-select --install
```

</div>

## 3. Make directory

Then, you need to make a directory for your project. The name can be anything, `project`, `cpp`, etc. In my case, I want to study algorithm via C++, so I make one named `algorithm`.

<div class="notice--primary" markdown="1">

`Make a directory for project`

```bash
$ mkdir algorithm
```

</div>

## 4. VScode Extension

To use C++ at Visual Studio Code, you need to install two extensions below. Before we move on next step, make an example file for it. In my case, I write `hello_world.cpp` for test.

1. `C/C++`
2. `Code Runner`

<div class="notice--primary" markdown="1">

`hello_world.cpp`

```cpp
#include <iostream>
using namespace std;

int main()
{
  cout << "Hello, world!" << endl;
  return 0;
}
```

</div>

### 4.1. Code Runner

Now, you need to modify some settings for Code Runner.

1. Jump to the setting with the gear icon of Code Runner, `Extension Settings`
2. Activate `Whether to run code in Integrated Terminal` in `Code-runner: Run In Terminal`
3. Jump to `settings.json` via clicking `Edit in settings.json` in `Code-runner: Executor Map`
4. Add commands below in the settings

<div class="notice--primary" markdown="1">

`settings.json`

```json
"code-runner.executorMapByGlob": {
        "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "cpp": "cd $dir && g++ -std=c++14 $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
    }
```

</div>

## 5. Debugging

If you want to debug in VScode, you need to generate `launch.json` and `tasks.json` files. First, click a gear icon next to the run icon in your `.c` or `.cpp` file. Then, select `g++ build and debug active file`. As a result, `launch.json` file is generated. Next, select `g++ build and debug active file` again, and `tasks.json` file will be generated. Now, you can debug your C++ file. If you want to support latest versions of it, add `"-std=c++14"` right below `"-g"`.
