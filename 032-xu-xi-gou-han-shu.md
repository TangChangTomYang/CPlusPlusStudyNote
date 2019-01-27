#### 虚 析构函数

1、 含有虚函数的类, 应该将析构声明为 虚函数 (虚析构函数)

2、 delete 父类指针, 才会调用子类的析构函数, 保证析构的完整性.



```

#include <iostream>
using namespace  std;

class Person{
    int m_age;
public:
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

int main( ) {
    
//    Person *pson = new Student();
//    pson-> run();
//    delete  pson;
    /** 打印结果:
     Person::Person()
     Student::Student()
     
     void Student::run()
     
     ~Person::Person()

     1> 可以发现 析构的流程是正确的, run 方法也是调用的Student 的方法是正确的
     2> 但是析构函数是错误的, 没有调用Student的析构, 只是调用了 Person的析构, 这时因为没有把析构函数定义为 虚析构函数, 非析构函数的调用 只与调用方法当时的指针类型有关系, 和指向的对象的真实类型无关
     */
    
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
