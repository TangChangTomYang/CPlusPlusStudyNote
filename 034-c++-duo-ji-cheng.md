####  C++ 多继承

**C++  允许一个类继承多个父类(不建议使用, 会增加程序设计复杂度),如下:**




<br>
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
**其实, C++ 中的多继承, 就是让一个类 具备多种特质, 类似于java 中的接口, OC 中的协议.**







<br>
#### 二、多继承体系下的构造函数调用

```
class Student{
    int m_score;
public:
    Student(int score){
        m_score = score;
        cout << "Student::Student(int score)"<< endl;
    }
};

class Worker{
    int m_salary;
public:
    Worker(int salary){
        m_salary = salary;
        cout << "Worker::Worker(int salary)" << endl;
    }
};

class Undergraduate : public Student, public Worker{
public:
    Undergraduate(int score,int salary): Student(score), Worker(salary) {
        cout << "Undergraduate::Undergraduate(int score,int salary)" << endl;
    }
    
};

```


<br>
#### 三、多继承 虚函数

**如果子类继承的多个父类都有虚函数, 那么子类对象就会产生对应的多张虚表**

```
class Student{
public:
    virtual void study(){ // 虚函数,是用来实现多态的
        cout << "Student::study()"<< endl;
    }
};

class Worker{
public:
    virtual void work(){
        cout << "void Worker::work()"<< endl;
    }
};

class Undergraduate : public Student, public Worker{
public:
void study(){
    cout << "void Undergraduate::study()"<< endl;
}

void work(){
    cout << "void Undergraduate::work()" << endl;
}

void play(){
    cout << "void Undergraduate::play()" << endl;
}

};
```

![](/assets/Snip20190128_1.png)

