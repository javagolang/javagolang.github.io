---
layout:     post
title:      cpp碎片学习
subtitle:   加强cpp各类知识点
date:       2019-10-31
author:     Datoucai
header-img: img/guigui-title.jpg
catalog: true
tags:
    - cpp

---

### 父类和子类相关

#### 子类对于父类函数的覆盖

i.e.
```cpp
class A:{
public:
  void Func(){
    std::cout << "HELLO A" <<std::endl;
  }
}

class B public A:{
public:
  void Func(){
    std::cout << "HELLO B" << std::endl;
  }
}
```
子类会覆盖父类同名成员函数

子类若有形参/名字均与父类相同的方法实现, 那么此方法将会覆盖父类的方法

实例化子类后在调用时会调用子类的成员函数，

如果想要调用父类的函数，则需要显示的调用 **父类::Func**


#### 成员函数的缺省参数

成员函数的缺省参数需要在函数生命使赋予默认值，而不能在实现时重新覆盖该缺省参数
