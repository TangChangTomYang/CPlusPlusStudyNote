#### 纯虚函数 和 抽象类




<br>
#### 一、纯虚函数

**1、 纯虚函数:** 没有函数体且初始化为0的虚函数,称之为纯虚函数.纯虚函数的作用是用来定义接口的, 类似于java中的接口和OC 中的协议.


```
class Animal{
public:
    // 定义纯虚函数,没有函数体{}, 且初始化为0
    virtual void run() = 0; 
};
```





<br>
#### 二、抽象类 (Abstract Class)

**1、 什么是抽象类?**
凡是,包含有纯虚函数的类, 都称之为抽象类

**2、抽象类的特点:**
1> 抽象类(含有纯虚函数的类), 不可以实例化
2> 抽象类可以包含非纯虚函数
3> 如果父类是抽象类, 子类没有完全实现父类的纯虚函数, 那么这个子类依然是抽象类, 即自由有纯虚函数的类就是抽象类

```
class Person{ // 抽象类, 不可实例化
public:
    virtual void run()=0; // 纯虚函数, 用作定义接口
    virtual void speak()=0; // 纯虚函数, 用作定义接口
    void doWork(){
        cout << "抽象类, 也可以有,非纯虚函数" << endl;
    }
};

class Student : public Person{ // 依然是抽象类
    void run(){
        cout << " void Student::run()" << endl;
    }
};

class GoodStudent : public Person{ // 非抽象类, 可以实例化
     void speak(){
         cout << "void GoodStudent::speak()" << endl;
     }
};

```

