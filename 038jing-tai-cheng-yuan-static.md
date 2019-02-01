#### 静态成员 (static)


<br>
#### 一、静态成员介绍

**1、静态成员 (static) **

在类中被 **static** 修饰的成员变量/ 函数, 都被称为静态成员.可以通过**对象**(对象.静态成员)/ **对象指针**(对象指针->静态成员)/ **类名** (类名::静态成员) 来访问,静态成员.


**2、静态成员变量**
1> 静态成员变量,**存储在数据段**(全局区,类似于全局变量), 整个程序运行过程中只有一份.
2> 静态成员变量相比于全局变量,它可以设定访问权限**(public/ private/ peotected)**达到局部共享的目的, 且静态成员的作用于在类里面.
3> 静态成员变量, **必须在类外面初始化**, 初始化时不能带 static ,如果类的声明和实现分离,那么**必须在类的 .cpp 文件中初始化**.

```
#include <iostream>
using namespace std;
class Car{

public:  // 静态成员可以使用 public/ protected/ privated 修饰访问权限
    static int m_price; // 静态成员变量
    int m_wheelCout; // 非静态成员变量
    
public: // 静态成员可以使用 public/ protected/ privated 修饰访问权限
   static void run(){ // 静态成员函数
       cout << "static void run()" << endl;
    }
    
    void display(){ // 非静态成员函数
        cout << "void display()" << endl;
    }
    
};

// 必须在类外面初始化,静态成员变量
int  Car::m_price = 20;

int g_age; // 全局变量, 编译器默认会在前面添加 static  修饰, 相当于 static int g_age;
void test(){ // 全局函数,编译器默认会在前面添加 static  修饰
    
}


int main( ) {
    //1. 通过对象访问 静态成员变量
    Car car1;
    car1.m_price = 30;
    cout << "car1.m_price: " <<  car1.m_price << endl;
    
    //2. 通过对象指针,访问静态成员
    Car *car2 = new Car();
    car2->m_price = 40;
    cout << "car2->m_price: " <<  car2->m_price << endl;
    
    //3. 通过类名访问 静态成员变量
    Car::m_price = 50;
    cout << "Car::m_price: " <<  Car::m_price << endl;
    
    /** 打印结果
     car1.m_price: 30
     car2->m_price: 40
     Car::m_price: 50
     */
    
    getchar();
    return 0;
}
```


**3、静态成员函数**
1> 静态成员函数内部不能使用this 指针 (this 指针只能在非静态成员函数内部使用).
2> 静态成员函数,不能是虚函数(虚函数只能是非静态函数)
3> 内部不能访问费静态成员变量/成员函数, 只能访问静态的成员变量/ 静态函数.
4> 非静态成员函数内部可以访问静态成员变量/ 静态函数
5> 构造函数/ 析构函数不能是静态函数
6> 当声明和实现分离时, 实现的部分不能带 static.

**4、静态成员变量的使用情景**

```
//静态成员变量的使用场景
class Person{
private:
    static int m_PersonCount; // 统计现有有多少人
    
public:
    
    static int currentPersonCount(){ // 静态成员方法
        return m_PersonCount;
    }
    
    Person(){ // 统计当前有多少人,出生一个就多一个
        m_PersonCount ++;
    }
    
    ~Person(){ // 死亡一个就少一个
        m_PersonCount --;
    }
    
};
int Person::m_PersonCount = 0 ;

int main( ) {
  
    Person pson1;
    Person *pson2 = new Person();
    cout << "当前有: "<< Person::currentPersonCount() <<"人" << endl;
    
    getchar();
    return 0;
}
```



