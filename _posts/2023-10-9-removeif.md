---
layout:       post
title:        "C++ remove_if的实现原理"
author:       "zxg"
header-style: text
catalog:      true
tags:
    - C/C++
---

## C++ remove_if的实现原理

```cpp
template<class ForwardIt, class UnaryPredicate>
ForwardIt remove_if(ForwardIt first, ForwardIt last, UnaryPredicate p)
{
    first = std::find_if(first, last, p);
    if (first != last)
        for (ForwardIt i = first; ++i != last;)
            if (!p(*i))
                *first++ = std::move(*i);  // 注意first先用后加
    return first;
}
// *p++等价于*(p++), ++是后执行的指令
```

其实好理解，两个指针，一个指针i扫描，另一个指针first指向待更新的位置，如果i指向的值不满足条件，则需要保留，即将它插入到first指向的位置，然后first后移。

最终first指向的位置为待删除的第一个元素位置！

cl巨人，你直说不行吗？绕一大圈子
