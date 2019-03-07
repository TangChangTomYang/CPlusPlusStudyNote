#### 静态成员 (static)


<br>
#### 一、静态成员介绍

**1、什么是静态成员  ? **
**凡是在类中被 `static` 修饰的 `成员变量/ 函数`, 都被称为静态成员.**


<br>
**2、静态成员的访问方式(3中)**
- **1> 通过类对象访问: `(对象.静态成员)` **
- **2> 通过指向对象的指针访问: `(对象指针->静态成员)`** 
- **3> 通过类名访问(域访问): `(类名::静态成员)`**
 

<br>
**3、静态成员变量的特点**
- **1> 静态成员变量和全局变量一样,都是存储在数据段`(全局区,类似于全局变量)`, 整个程序运行过程中只有一份.**
- **2> 与全局变量不同的是, 静态成员变量可以设定访问权限,如: `(public/ private/ peotected)` 达到局部共享的目的, 且静态成员的作用于在类里面.**
- **3> 静态成员变量, `必须在类外面初始化, 初始化时不能带 static 修饰` ,如果类的声明和实现分离,那么`必须在类的 .cpp 文件中初始化`**.




**3、静态成员函数**
1> 静态成员函数内部不能使用this 指针 (this 指针只能在非静态成员函数内部使用).
2> 静态成员函数,不能是虚函数(虚函数只能是非静态函数)
3> 内部不能访问费静态成员变量/成员函数, 只能访问静态的成员变量/ 静态函数.
4> 非静态成员函数内部可以访问静态成员变量/ 静态函数
5> 构造函数/ 析构函数不能是静态函数
6> 当声明和实现分离时, 实现的部分不能带 static.




**示例代码**
```
#include <iostream>
using namespace std;
class Car{

public: // 静态成员可以使用 public/ protected/ privated 修饰访问权限
static int ms_price; // 静态成员变量
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
int  Car::ms_price = 20;

int g_age; // 全局变量, 编译器默认会在前面添加 static  修饰, 相当于 static int g_age;
void test(){ // 全局函数,编译器默认会在前面添加 static  修饰
    
}


int main( ) {
    //1. 通过对象访问 静态成员变量
    Car car1;
    car1.ms_price = 30;
    cout << "car1.ms_price: " <<  car1.ms_price << endl;
    
    //2. 通过对象指针,访问静态成员
    Car *car2 = new Car();
    car2->ms_price = 40;
    cout << "car2->ms_price: " <<  car2->ms_price << endl;
    
    //3. 通过类名访问 静态成员变量
    Car::ms_price = 50;
    cout << "Car::ms_price: " <<  Car::ms_price << endl;
    
    /** 打印结果
     car1.ms_price: 30
     car2->ms_price: 40
     Car::ms_price: 50
     */
    
    getchar();
    return 0;
}
```





**4、静态成员变量的使用情景1- 统计对象**

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



**5、 静态成员变量,不占用对象内存空间**
 
```
//静态成员变量不占对象内存
//C++ 中最小的类, 占用一个字节

class Person{
   static int ms_age;
};

int Person::ms_age = 0; //静态成员变量初始化

cout << sizeof(Person) << endl; // 结果 1字节
```

<br>

**6、静态成员 继承特点**

```

#include <iostream>
using namespace std;


class Person {
public:
    static int ms_age;
};

int  Person::ms_age = 0;
class Student : public Person{
    
};


int main( ) {
  
    cout << Person::ms_age << endl; //0
    
    Person pson;
    pson.ms_age = 10;
    cout << pson.ms_age << endl; //10
    
    Student stu;
    stu.ms_age = 20;
    cout << stu.ms_age << endl; // 20
    
    getchar();
    return 0;
}

```




<br>
#### 二、静态成员变量的经典实用案例----单例模式


C++中单例的使用
```
/** C++ 中的单例的使用
 1. 将 构造函数私有化, 不允许外部访问
 2. 定义一个 静态的 私有的 当前类指针
 3. 提供一个静态的成员函数公共的接口访问 这个静态的 私有的 当前类指针
 4. 如果有 销毁单例的要求, 需要再写一个 静态成员方法给外部访问 删除单例
 */
class TcpTool{
public:
   static TcpTool *shareTool(){ // 提供对外的 当前类指针接口
        if (ms_tool == NULL ) {
            ms_tool = new  TcpTool();
        }
        return ms_tool;
    }
    
    static void removeshareTool(){ // 提供对外的 当前类指针接口
        if (ms_tool == NULL ) {
            return;
        }
      
        delete ms_tool;
        ms_tool = NULL;
    }
private:
    static TcpTool *ms_tool ; // 2. 定义一个私有的 静态的 当前类对象指针
    TcpTool(){ //1. 构造函数私有化, 不允许外部访问
        cout << "TcpTool()" << endl;
    }
    
    ~TcpTool(){
        cout << "~TcpTool()" << endl;
    }
};
TcpTool *TcpTool::ms_tool = NULL ; // 静态成员初始化


int main( ) {
  
    cout << Person::ms_age << endl; //0
    
    Person pson;
    pson.ms_age = 10;
    cout << pson.ms_age << endl; //10
    
    Student stu;
    stu.ms_age = 20;
    cout << stu.ms_age << endl; // 20
    
    TcpTool *tool = TcpTool::shareTool();
    TcpTool::removeshareTool();
    TcpTool *tool2 = TcpTool::shareTool();
    TcpTool::removeshareTool();
    TcpTool *tool3 = TcpTool::shareTool();
    TcpTool::removeshareTool();
    TcpTool *tool4 = TcpTool::shareTool();
    TcpTool::removeshareTool();
    
    getchar();
    return 0;
}
```



#### 三 、 C++ 和 C 语言中防止野指针
```
int *p = new int();

delete p;
p = NULL ;
```
