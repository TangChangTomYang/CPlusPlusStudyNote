#### 父类的构造函数


#### 一子类的构造函数,默认会调用父类的构造函数

```
class Person {
    int m_age;
public:
    Person(int age = 10) : m_age(age){
        cout << "Person(int age = 10) : m_age(age) " << endl;
    }
};

class Student : public Person{
    int m_score;
public:
    Student(){ // 子类的构造函数, 默认会自动调用父类的构造函数
        cout << " Student() " << endl;
    }
};


int main() {
    Student *stu = new Student();
    delete  stu;
  
    getchar();
    return 0;
}
```