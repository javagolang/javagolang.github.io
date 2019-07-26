---
layout:     post
title:      TX2 install mxnet for cpp with cuda support [build from source]
subtitle:   tx2源码编译mxnet踩坑记录
date:       2019-07-25
author:     Datoucai
header-img: img/turtletitile2.jpg
catalog: true
tags:
    - mxnet


---

> 龟龟是最可爱的猫




Install mxnet for cpp package in TX2 is not that easy

Record here for my experience.

Steps:

Follow the documentation on this site [Install MXNet on a Jetson](http://mxnet.incubator.apache.org/versions/master/install/install-jetson.html) , there is a little  different

1. First clone mxnet from github && cd mxnet
    ```bash
    git clone --recursive https://github.com/apache/incubator-mxnet.git mxnet
    cd mxnet
    git submodule init
    git submodule update
    ```
    
2. Configure CUDA:
	```bash
	nvcc --version
	```
	on my TX2 is CUDA9.0

	```bash
	sudo rm /usr/local/cuda
	sudo ln -s /usr/local/cuda-9.0 /usr/local/cuda
	```

3. Copy **config.mk**
    ```bash
	  cp make/crosscompile.jetson.mk config.mk
	```

4. Edit config.mk, in **config.mk** , modify these settings:
	1) USE_CUDA_PATH = /usr/local/cuda
	2) USE_OPENCV = 1

   3) USE_JEMALLOC = 0 which is different from official guide but **VERY IMPORTENT**

   4) USE_JPERFTOOLS = 0 which is different from official guide but **VERY IMPORTENT

   5) USE_CPP_PACKAGE = 1 for cpp package

   6) Update the NVCC settings. NVCCFLAGS := -m64

   there 3 and 4 is important , or when you finish your build , using the mxnet api , you might get error like :
	  ```bash
	  src/tcmalloc.cc:284] Attempt to free invalid pointer
	  ```
   
5. in **3rdparty/mshadow/make/mshadow.mk**, change this setteing as follow:
	```bash
	MSHADOW_CFLAGS += -DMSHADOW_USE_PASCAL=1
	```
	
6. Something else:
   
   in **Makefile**, **limit the arch for tx2**, which is important. 
      	*KNOWN_CUDA_ARCHS := 62    # limit arch for tx2 here*
   
   ```bash
   ifeq ($(USE_CUDA), 1)
   ifeq ($(CUDA_ARCH),)
   	# KNOWN_CUDA_ARCHS := 30 35 50 52 60 61 70 75 
   	KNOWN_CUDA_ARCHS := 62    # limit arch for tx2 here
   	# Run nvcc on a zero-length file to check architecture-level support.
   	# Create args to include SASS in the fat binary for supported levels.
   	CUDA_ARCH := $(foreach arch,$(KNOWN_CUDA_ARCHS), \
   				$(shell $(NVCC) -arch=sm_$(arch) -E --x cu /dev/null >/dev/null 2>&1 && \
   						echo -gencode arch=compute_$(arch),code=sm_$(arch)))
   	# Convert a trailing "code=sm_NN" to "code=[sm_NN,compute_NN]" to also
   	# include the PTX of the most recent arch in the fat-binaries for
   	# forward compatibility with newer GPUs.
   	CUDA_ARCH := $(shell echo $(CUDA_ARCH) | sed 's/sm_\([0-9]*\)$$/[sm_\1,compute_\1]/')
   	# Add fat binary compression if supported by nvcc.
   	COMPRESS := --fatbin-options -compress-all
   	CUDA_ARCH += $(shell $(NVCC) -cuda $(COMPRESS) --x cu /dev/null -o /dev/null >/dev/null 2>&1 && \
   						 echo $(COMPRESS))
   endif
   $(info Running CUDA_ARCH: $(CUDA_ARCH))
   endif
   ```
   
   
   
   OR you might get error like :
   
   ```bash
   INFO: nvcc was not found on your path
   INFO: Using /usr/local/cuda-9.0/bin/nvcc as nvcc path
   Running CUDA_ARCH: -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_70,code=[sm_70,compute_70] --fatbin-options -compress-all
   
   ...
   
   DMXNET_USE_LIBJPEG_TURBO=0" src/operator/tensor/broadcast_reduce_op_value.cu
   Killed
   Makefile:471: recipe for target 'build/src/operator/tensor/ordering_op_gpu.o' failed
   make: *** [build/src/operator/tensor/ordering_op_gpu.o] Error 137
   make: *** Waiting for unfinished jobs....
   ```
   
7. when you finished your built and use its cpp api, you may meet error like this:
	
	*terminate called after throwing an instance of 'dmlc::Error'
	      what(): [01:20:54] /usr/include/mxnet-cpp/ndarray.hpp:236: Check failed: MXNDArrayWaitToRead(blob_ptr_->handle_) == 0 (-1 vs. 0)*
	
   
   
   ```bash
     terminate called after throwing an instance of 'dmlc::Error'
         what(): [01:20:54] /usr/include/mxnet-cpp/ndarray.hpp:236: Check failed: MXNDArrayWaitToRead(blob_ptr_->handle_) == 0 (-1 vs. 0)
   ```
   
   
      this is a problem on gpu mode, which is resulted of TX2 **out of memory**, change the input to a smaller one can solve.
   
   