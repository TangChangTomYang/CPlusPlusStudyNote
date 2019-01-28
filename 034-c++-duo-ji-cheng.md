####  C++ 多继承

C++  允许一个类可以有多个父类(不建议使用, 会增加程序设计复杂度),如下:


#### 一、 C++ 中的多继承示例
```
#include <iostream>
using namespace std;

// 学生
class Student {
public:
    int m_score;
    void study(){
        cout << "void Student::study()" << endl;
    }  
};

// 工人
class Worker{
public:
    int m_salary;
    void work{
        cout << "void Worker::work" << endl;
    }
};

// 大学生
class Undergraduate : public Student, public Worker{
public:
    int m_grade;
    void play(){
        cout << "void Undergraduate::play()" << endl;
    }
};


int main(){
    
    Undergraduate *ug = new Undergraduate();
    ug->m_score = 90;
    ug->m_salary = 999;
    ug->m_grade = 4;
    
    ug->study();
    ug->work();
    ug->play();
    
    return 0;
}

```
其实, C++ 中的多继承, 就是让一个类 具备多种特质, 类似于java 中的接口, OC 中的协议.

