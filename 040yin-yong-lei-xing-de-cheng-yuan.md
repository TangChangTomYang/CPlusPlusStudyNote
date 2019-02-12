#### 引用类型的成员

1、应用类型成员变量必须初始化(不考虑static 情况)

- 在声明引用类型成员变量时直接初始化
- 通过初始化列表初始化

```
class Person{
    int m_age;
    int &m_price = m_age; // 定义引用类型的成员变量时,直接初初始化
    int &m_height;
    
public:
    Person(int &age):m_height(age){ // 在构造函数的初始化列表中初始化 引用类型成员变量
        
    }
};
```