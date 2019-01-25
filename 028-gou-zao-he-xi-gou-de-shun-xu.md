#### 构造 析构的顺序

1、 构造和析构的顺序相反
```
#include<iostream>
using namespace std;

// 当调用构造函数初始化一个对象时,会先调用父类的构造函数, 再调用子类的构造函数
// 当一个对象销毁时, 会先调用子类的析构函数, 再调用父类的析构函数


class Person{
    int m_age;
public:
    Person(){
        m_age = 0;
        cout << " Person() " << endl;
    }
    
    ~Person(){
        cout << " ~Person() " << endl;
    }
};


class Student : public Person{
    int m_no;
public:
    Student(){
        m_no = 0;
        cout << " Student() " << endl;
    }
    
    ~Student(){
        cout << " ~Student() " << endl;
    }
};

int main( ) {
    Student *stu = new Student();
    delete stu;
    
    getchar();
    return 0;
}

/** 执行顺序
 Person()
 Student()
 ~Student()
 ~Person() 
 */
```