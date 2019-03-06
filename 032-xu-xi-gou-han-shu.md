#### 虚 析构函数




**1、 含有虚函数的类, 应该将 析构函数 声明为 虚函数 (虚析构函数)**

**2、 delete 父类指针, 才会调用子类的析构函数, 保证析构的完整性.**

**3 虚函数的特点:**
 - **1> 使用virtual 关键字修饰的函数 是虚函数**
 - **2> 有虚函数的类比无虚函数的类,  对象要大4个字节(或者8个字节)**
 - **3> 有虚函数的类, 对象的前4个字节(8个字节)存储的是虚表的地址**
 - **4> 虚函数,是C++实现函数多态的一种手段**




```
#include <iostream>
using namespace  std;

class Person{
    int m_age;
public:
    // 使用virtual 修饰的函数是虚函数
    virtual void run(){
        cout << "void Person::run()" << endl;
    }
    
    Person(){
        cout << "Person::Person()" << endl;
    }
    ~Person(){
        cout << "~Person::Person()" << endl;
    }
};

class Student : public Person{
    int m_no;
public:
    void run(){
        cout << "void Student::run()" << endl;
    }
    Student(){
        cout << "Student::Student()" << endl;
    }
    // 虚析构函数
    virtual ~Student(){
        cout << "~Student::Student()" << endl;
    }
};


class GoodStudent : public Student{
    int m_no;
public:
    void run(){
        cout << "void Student::run()" << endl;
    }
    GoodStudent(){
        cout << "GoodStudent::GoodStudent()" << endl;
    }
    ~GoodStudent(){
        cout << "~GoodStudent::GoodStudent()" << endl;
    }
};
```

**测试**
```

int main( ) {
    
//    Person *pson = new Student();
//    pson-> run();
//    delete  pson;
}
```

**打印结果:**
```
 Person::Person()
 Student::Student()
 
 void Student::run()
 ~Person::Person() // student 没有析构
```

- **1> 可以发现 构造的流程是正确的(Student/ Person都构造了), run 方法也是调用的Student 的方法是正确的**

- **2> 但是 析构函数是错误的, 没有调用Student的析构, 只是调用了 Person的析构, 这时因为没有把(Person)析构函数定义为 虚析构函数**

- **3> 非析构函数的调用 只与调用方法当时的指针类型有关系, 和指向的对象的真实类型无关**
   
  
  
 <br>
**测试** 
```
int main( ) {

    Student *stu = new GoodStudent();
    stu -> run();
    delete  stu;
    /** 打印结果:
     Person::Person()
     Student::Student()
     GoodStudent::GoodStudent()
     void Student::run()
     // 虚析构函数, ok
     ~GoodStudent::GoodStudent()
     ~Student::Student()
     ~Person::Person()
     */
    
    
    getchar();
    return 0;
}
```


**结论:**
** 1> 有虚函数的类, 必须把析构函数也定义为虚析构函数**