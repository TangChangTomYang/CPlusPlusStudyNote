#### 构造函数的相互调用

**1、在C++ 中, 构造函数是不允许相互调用的.
2、如果在构造函数中强行调用另一个构造函数,会错误的产生临时对象, 这会导致逻辑错误.
3、如果一个构造函数想要调用另一个构造函数, 那么必须在初始化列表中使用**

示例如下:
```
struct Person{
    int m_age;
    double m_height;
    
    Person() : Person(0,0){  // 正确的写法
//        Person(0,0); 错误写法, 构造函数互相调用只能是 在初始化列表中调用
//        这种错误的写法会 产生一个临时的对象
    }
    
    Person(int age , double height ) : m_age(age), m_height(height){
    }
};
```