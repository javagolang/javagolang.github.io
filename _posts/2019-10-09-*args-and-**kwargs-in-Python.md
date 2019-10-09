---
layout:     post
title:      python中的 *args和**kwargs
date:       2019-10-09
author:     Datoucai
header-img: img/turtlrtitle3.jpg
catalog: true
tags:
    - python


---

> 龟龟是最可爱的猫

## python中的*args和**kwargs学习

### \*args
- \*args是用来传递一个可变数量的参数，它是non-keyworded的
- 其实用**\***代表这个数目可变的参数列表， 但是通常我们使用\*args
- \*args使得我们可以向之前定义好的函数中传入比之前定义的更多的参数

- 使用**\***，意味着**\***所关联的变量成为一个可迭代的变量

**Example for usage of \*arg:**
```python
def myFun(*argv):  
    for arg in argv:  
        print (arg)

myFun('Hello', 'turtle', 'i am your fans')  
```
运行结果：
```bash
Hello
turtle
i am your fans
```

### \**kwargs

- \**kwargs是一个关键词式的，长度可变的参数列表

- \**kwargs类似于字典结构，key-value格式，因此他在迭代的时候打印出来没有固定顺序

```python
def myFun(arg1, arg2, arg3):
	print("arg1:", arg1)
	print("arg2:", arg2)
	print("arg3:", arg3)

# Now we can use *args or **kwargs to
# pass arguments to this function :
args = ("Geeks", "for", "Geeks")
myFun(*args)

kwargs = {"arg1" : "Geeks", "arg2" : "for", "arg3" : "Geeks"}
myFun(**kwargs)
```

结果：
```bash
arg1: Geeks
arg2: for
arg3: Geeks
arg1: Geeks
arg2: for
arg3: Geeks
```
