---
layout:     post
title:      Using clang for cpp/cc compile
subtitle:   clang replace gcc
date:       2019-07-16
author:     大头菜turtle
header-img: img/guigui-title.jpg
catalog: true
tags:
    - OpenCV

---

> 感谢[Huxpro](https://github.com/huxpro)提供的博客模板
>

### clang VS gcc

when return boolean, such as:

```cpp
bool Init(){
    // do something 
}
```

in  **gcc** you can  return nothing, but in **clang**  you must return a boolean value. Or clang will throw segmentation fault

Code must be:

```cpp
bool Init(){
    // do something
    return true; //or return false
}
```



### How to replace gcc with clang in unix

- first install llvm and clang:

  ```bash
  sudo apt install llvm
  sudo apt insatll clang
  ```

- change default c++ 

  for cpp:

  ```bash
  sudo update-alternatives --config c++
  
  There are 2 choices for the alternative c++ (providing /usr/bin/c++).
  
    Selection    Path              Priority   Status
  ------------------------------------------------------------
    0            /usr/bin/g++       20        auto mode
    1            /usr/bin/clang++   10        manual mode
  * 2            /usr/bin/g++       20        manual mod
  
  Press enter to keep the current choice[*], or type selection number: 1
  ```

  c in the same way:

  ```bash
  sudo update-alternatives --config cc
  There are 2 choices for the alternative cc (providing /usr/bin/cc).
  
    Selection    Path            Priority   Status
  ------------------------------------------------------------
    0            /usr/bin/gcc     20        auto mode
    1            /usr/bin/clang   10        manual mode
  * 2            /usr/bin/gcc     20        manual mode
  
  Press <enter> to keep the current choice[*], or type selection number: 1
  update-alternatives: using /usr/bin/clang to provide /usr/bin/cc (cc) in manual mode
  ```

  OK, Now you use clang instead of gcc/g++

