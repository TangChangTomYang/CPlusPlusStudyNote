#### 父类的构造函数

<br>
#### 一、默认情况下, 如果父类有无参构造函数且子类没有显示的调用父类的其它构造函数, 子类会自动调用父类的无参构造函数

```
class Person {
    int m_age;
public:
    Person(){
        cout << "Person() " << endl;
    }
};

class Student : public Person{
    int m_score;
public:
    //父类有无参的构造函数, 子类没有显示的调用父类的构造函数的化, 系统会自动调用父类的 无参 构造函数
    Student(){ // 会自动调用父类无参构造
        cout << "Student() " << endl;
    }
    
    Student(int score){// 会自动调用父类无参构造
        cout << "Student(int score)" << endl;
    }
};

int main() {
    Student *stu1 = new Student();
    Student *stu2 = new Student(10);
    delete stu1; // 会自动调用父类无参构造
    delete stu2; // 会自动调用父类无参构造
  
    getchar();
    return 0;
}
```





<br>
#### 二、如果父类只有, 有参的构造函数, 那么子类必须 显示的实现自己的构造函数且在自己的构造的初始化列表调用父类的有参构造函数

```
class Animal {
    int m_sex;
public:
    
    Animal(int sex) : m_sex(sex){
        cout << "Animal(int sex) : m_sex(sex)" << endl;
    }
};

class Dog : public Animal{
    int m_age;
public:
    Dog():Animal(0){// 必须显示调用父类有参构造函数
        
    }
    Dog(int age): m_age(age), Animal(0){// 必须显示调用父类有参构造函数
        
    }
   
};

int main() {
   
     // 情景1
    Dog *d1 = new Dog();
    Dog *d2 = new Dog(10);
    delete d1;
    delete d2;

    getchar();
    return 0;
}

```


**注意:
构造函数调用构造函数,必须使用初始化列表**







