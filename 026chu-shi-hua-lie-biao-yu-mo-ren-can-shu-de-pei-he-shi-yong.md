#### 初始化列表与默认参数的配合使用


<br>
#### 一、 构造函数初始化列表+默认参数, 可以达到函数重载的效果

如下:
```
class Person {
    int m_age;
    double m_height;
public:
    // 构造函数,初始化列表和默认参数一起用, 达到多个函数重载的效果
    Person(int age = 0, double height = 1.1) : m_age(age), m_height(height){
        cout << "Person(int age = 0, double height = 1.1) : m_age(age), m_height(height)" << endl;
    }
};

int main() {
    // 构造函数初始化列表与默认参数,达到函数重载的效果
    Person *p1 = new Person();
    Person *p2 = new Person(1);
    Person *p3 = new Person(1,2.0);
    delete p1;
    delete p2;
    delete p3;
    
    getchar();
    return 0;
}

```



<br>
#### 二、构造函数的声明和实现分开情况

1、初识化列表只能写在函数的实现中.
2、默认参数只能写在函数的声明中.

```
.hpp 文件声明
namespace YR  {
    class Student{
        int m_age;
        double m_height;
    public:
        Student(int age = 10, double height = 1.88); // 默认参数只能写在函数的声明
        
    };
}


.cpp 文件实现
namespace YR  {
    // 初始化列表只能写在函数的实现部分
    Student::Student(int age , double height ) : m_age(age), m_height(height){
        
    }
}
```
