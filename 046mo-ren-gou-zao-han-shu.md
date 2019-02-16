#### 默认构造函数


**1、说明: **
默认构造函数, 也叫编译器自动为类生成的无参构造函数


**2、 C++ 编译器在某些情况下(如下:),会给类自动生成无参的构造函数**

- **1> 成员变量在声明的同时进行了初始化.**
  ```
  class Animal{ // 编译器 不会为Animal类, 自动生成无参的构造函数
      int m_type;
  };
  
  class Person : public Animal{ // 编译器会为Person类, 自动生成无参的构造函数
    int m_age = 0; // 声明的同时进行初始化
  };
  ```
  
- **2> 有生成虚函数 (virtual 函数 -- 多态/ 虚表)**
  ```
  class Car{ // 编译器会为Car类, 自动生成无参的构造函数
    int m_price;
public:
    virtual void run(){ //虚函数(多态/ 虚表)
        
    }
};
```

- **3> 虚继承了其它类 `class xxx : virtual public yyy`**

    ```
    // virtual 虚继承,解决菱形继承的问题
    class Student : virtual public Animal{// 编译器会为Student类, 自动生成无参的构造函数
        int m_score;
        
    };
    ```