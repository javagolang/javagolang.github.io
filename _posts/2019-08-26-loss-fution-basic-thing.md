---
layout:     post
title:      CNN Learning （2
subtitle:   basic knowledge for cnn loss fuction
date:       2019-08-26
author:     Datoucai
header-img: img/guigui-title.jpg
catalog: true
tags:
    - CNN

---


> 龟龟是最可爱的小猫咪

## 关于正则化

对于一个线性分类来说，训练目的是找出一个权重矩阵使得loss fuction接近于0，假设有这样一个权重矩阵W满足条件，那么倍增W可能仍然满足条件。

这当然不是我们想要看到的，那么为了规避这种情况，可以给loss fuction加上惩罚项，如L2规范化（正则化）

### L2 正则化
L2翻数的定义：
![zhihu](https://pic2.zhimg.com/80/v2-b1fc63fb060cb7ccf6d040bc7e675a95_hd.png "L2 Regularization")

或者可以写成

![L2 Regularization](https://latex.codecogs.com/gif.latex?R%28W%29%3D%5Csum_%7Bk%7D%5E%7B%20%7D%5Csum_%7Bl%7D%5E%7B%20%7Dw_%7Bk%2Cl%7D%5E%7B2%7D "l2 Regularization")

R(W)=\sum_{k}^{ }\sum_{l}^{ }w_{k,l}^{2}
