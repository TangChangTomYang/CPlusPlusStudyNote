#### C++ 中的初始化列表


**1、 什么是初始化列表? **
1> 初始化列表是一种便捷的成员变量初始化方式
2> 初始化列表是C++ 的一种特性, C 语言没有这种特性.
3> 初始化列表只能用在C++ 的构造函数中.
如下: 
```
struct Person{
    int m_age;
    double m_height;
    
    //这是一般的构造函数写法
    //Person(int age, double height){
    //    this -> m_age = age;
    //    this -> m_height = height;
    //}
    
    // 使用初始化列表,来初始化构造函数
    //Person(int age, double height) : m_age(age), m_height(height){ 
    
    // 上面的 m_age(age) 就相当于 this->m_age = age;// 初识化的值 可以是任何表达式
    }
}

```

