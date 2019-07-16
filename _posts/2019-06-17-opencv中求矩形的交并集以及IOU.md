---
layout:     post
title:      使用opencv找rect的交并集
subtitle:   快速求iou
date:       2019-06-27
author:     Datoucai
header-img: img/guigui-title.jpg
catalog: true
tags:
    - OpenCV

---

> 感谢[Huxpro](https://github.com/huxpro)提供的博客模板
>
> 龟龟是最可爱的猫

#### 使用opencv可以轻易获取两个矩形的IOU



两个矩形分别为：

```c++
cv::Rect rect1;
cv::Rect rect2;
```

求交集：

```cpp
cv::rect_result = rect1 & rect2
```

