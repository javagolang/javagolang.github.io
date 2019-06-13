照着官网教程做的时候执行catkin_make命令时报错

 ```bash
CMakeLists.txt:52 (find_package)
Configuring incomplete, errors occurred!
See also "/home/xxx/catin_ws/build/CMakeFiles/CMakeOutput.log".
See also "/home/xxx/catin_ws/build/CMakeFiles/CMakeError.log".
Invoking "cmake" failed
```

解决方案：

```bash
pip install -U rosdep rosinstall_generator wstool rosinstall six vcstools
```

