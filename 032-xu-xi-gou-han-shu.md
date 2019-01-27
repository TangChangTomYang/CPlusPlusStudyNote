#### 虚 析构函数

1、 含有虚函数的类, 应该将析构声明为 虚函数 (虚析构函数)

2、 delete 父类指针, 才会调用子类的析构函数, 保证析构的完整性.



```
#include <isstream>
using namespace std;

class Person{
    int m_age;
public:
    // 定义函数为虚函数
    virtual void run(){
        cout << "void Person::run()" << endl;
    }
    
    // 定义了虚函数的类, 必须将析构函数也定义为虚析构函数
    virtual ~Person(){
        cout << "Person::~Person()" << endl;
    }
};

class Student : public Person{
    int m_no;
public:
    void run(){
        cout << "void Student::run()" << endl;
    }
    
    ~Student(){
        cout << "Student::~Student()" << endl;
    }
}
```
