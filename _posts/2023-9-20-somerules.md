## C++多继承下的地址问题

```cpp
class ClassA { 
public: 
    virtual ~ ClassA(){}; 
    virtual void FunctionA(){}; 
}; 


class ClassB { 
public: 
    virtual void FunctionB(){}; 
}; 


class ClassC : public ClassA,public ClassB { 
public: 
}; 

ClassC cObject; 
ClassA* pA = &cObject; 
ClassB* pB = &cObject; 
ClassC* pC = &cObject; 
```

对象c的数据成员依次如下：

| A类数据成员 |

| B类数据成员 |

| C类数据成员 |

所以对象c既是一个classA也是一个ClassB

向上转换为ClassA时，指针指向ClassA部分，所以pa和pc指向的地址相同

而pb和这两者都不同。
