---
layout:     post
title:     Using gdb debug core_dump in cmake
date:       2019-08-26
author:     Datoucai
header-img: img/turtlrtitle3.jpg
catalog: true
tags:
    - cnn


---

> 龟龟是最可爱的猫

### Using Cmake to generate gdb core file

in CMakeLists.txt:
```bash
SET(CMAKE_BUILD_TYPE "Debug")
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall
```

then rebuild your project

### Generate core file when meet a _core dump_
```bash
ulimit -c
```
if reult is '0', no coredump file will be generated

then :
```bash
ulimic -c unlimited
```

```bash
cd /
mkdir corefile    ## corefile saving path
echo "/corefile/core-%e%-p%-%t" > /proc/sys/kernel/core_pattern    ##change corefile saving path
```

### Using gdb to debug core dump
```bash
gdb [your_program] [core_file]
```
