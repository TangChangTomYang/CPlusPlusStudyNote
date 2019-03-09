#### 默认构造函数


**1、什么是默认构造函数? **
**默认构造函数, 也叫编译器自动为类生成的无参构造函数**


<br>
**2、C++ 编译器在某些情况下,会给类自动生成无参的构造函数**

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
    
- **4> 包含了对象类型(非指针类型)的成员, 且这个成员有构造函数**
    ```
    class Dog { // 编译器不会为Dog类生成无参的构造函数
        int m_age;
    };
    
    class Girl : public Dog{ // 编译器不会为Girl类生成无参的构造函数, 因为Dog 无构造函数
        Dog dog;
    };
    
    //
    class Car{ // 编译器会为Car类, 自动生成无参的构造函数
        int m_price;
    public:
        virtual void run(){ //虚函数(多态)
            
        }
    };
    
    class Worker{ // 编译器会自动为Worker自动生成无参的构造函数, 因为有对象类型成员car,且car有构造函数
        Car car;
    };
    ```
    
- **5> 父类有构造函数(不论是系统自动生成的,还是程序员手动添加的)**
    ```
    class Person {
        int m_age;
    public:
        Person(){
        }
    };
    
    class Student : public Person{ // 编译器会自动为Student 生成无参构造函数, 因为父类Person 有构造函数
        int m_score;
    }
    ```
    
**3、结论:**
对象创建后, 需要做一些额外的操作(比如: 内存操作/ 函数调用), 编译器一般会自动为其生成无参的构造函数