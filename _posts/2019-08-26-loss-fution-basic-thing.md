---
layout:     post
title:      CNN Learning（2)
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

这当然不是我们想要看到的，那么为了规避这种情况，可以给loss fuction加上正则惩罚项，如L2规范化（正则化）

### L2 正则化
L2翻数的定义：
![zhihu](https://pic2.zhimg.com/80/v2-b1fc63fb060cb7ccf6d040bc7e675a95_hd.png "L2 Regularization")

或者可以写成

![L2 Regularization](https://latex.codecogs.com/gif.latex?R%28W%29%3D%5Csum_%7Bk%7D%5E%7B%20%7D%5Csum_%7Bl%7D%5E%7B%20%7Dw_%7Bk%2Cl%7D%5E%7B2%7D "l2 Regularization")

以SVM的henge loss为例，加上L2正则项之后的损失函数为：

![loss fuction](https://latex.codecogs.com/gif.latex?L%20%3D%20%5Cunderbrace%7B%20%5Cfrac%7B1%7D%7BN%7D%20%5Csum_i%20L_i%20%7D_%5Ctext%7Bdata%20loss%7D%20&plus;%20%5Cunderbrace%7B%20%5Clambda%20R%28W%29%20%7D_%5Ctext%7Bregularization%20loss%7D%20%5C%5C%5C%5C)

损失函数由两部分组成，一部分是由数据决定的**data loss**, 另一部分是与数据无关的仅仅由权重本身所决定的正则损失项**Regularization loss**，乘以一个L2正则系数λ，通常由cross-valiadation决定

展开就是：
![expand](https://latex.codecogs.com/gif.latex?L%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%5Csum_i%20%5Csum_%7Bj%5Cneq%20y_i%7D%20%5Cleft%5B%20%5Cmax%280%2C%20f%28x_i%3B%20W%29_j%20-%20f%28x_i%3B%20W%29_%7By_i%7D%20&plus;%20%5CDelta%29%20%5Cright%5D%20&plus;%20%5Clambda%20%5Csum_k%5Csum_l%20W_%7Bk%2Cl%7D%5E2 "expand loss fuction")

L2惩罚在同等情况下更倾向于选择出更小更均匀（漫反射状）的权重，避免个别维度的权重过大，一定程度上可以改善过拟合。
