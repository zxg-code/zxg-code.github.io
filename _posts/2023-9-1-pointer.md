---
layout:       post
title:        "C中*和其他符号或关键字的结合"
author:       "zxg"
header-style: text
catalog:      true
tags:
    - C/C++
---

### 关于指针

- 指针和一些符号结合时的优先级
  
  ```cpp
  int p;    // int型变量
  int* p;    // 一个指针，指向int型
  int** p;    // 指针的指针
  int p[3];    // 一个数组，存放int型
  // p先与[]结合，表示p先是一个数组，再和*结合，即一个存放指针的数组
  int* p[3];
  // 括号优先级最高，(*p)表示p先是一个指针，
  // 再和[3]结合，表示指针指向的是一个大小为3的数组，
  // 然后再看int，表示数组内容为int类型
  // 即p是一个指向数组int[3]的指针
  int (*p)[3];
  int p(int);  // 函数
  // 括号优先级最高，所以p先是一个指针，
  // 然后和（int)结合，说明指针指向一个函数（参数为int),
  // 再看外面的int，说明函数返回值为int.
  // 即p是一个指向参数为int，返回值为int的函数的指针
  int (*p)(int);
  // 首先看最里面，p先与(int)结合，成为一个参数为int的函数，
  // 再看*，说明函数返回值为指针，
  // 所以记内部 (*p(int)) = ptr为一个函数，
  // 剩余部分int* ptr[3]
  // 根据上述内容，ptr是一个存放int指针的数组
  // 综上，p是一个函数，函数参数为int，返回值是一个指针，
  // 该指针指向一个存放int指针的数组
  int* (*p(int))[3];
  ```

- 关于const 和*
  
  **const总是和它左边的结合，左边不存在内容时才和右边的结合**
  
  ```cpp
  // const修饰右边的int，所以a是一个指向常量的指针
  // 这种形式不如下面这个形式好理解
  const int* a; 
  // 该形式与上述形式等价
  // const修饰左边的int，所以a是一个指向常量的指针
  int const *a;
  
  // const修饰左边的指针，所以a是一个常指针
  int* const a;
  ```