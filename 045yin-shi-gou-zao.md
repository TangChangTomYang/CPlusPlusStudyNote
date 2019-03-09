#### 隐式构造


**1、 什么是隐式构造/ 或者什么叫做隐式构造? **
**所谓隐式构造, 就在明面上我们的代码看上去是不会触发构造函数产生一个新对象, 实际上编译器却悄悄的调用了构造函数产生了对象, 这种行为我们成为隐式构造**

<br>
**2、C++中, 什么情况会触发隐式构造**
- **1> 在C++ 中,如果在定义类时有定义单参数构造函数, 那么在使用时,直接将单参数构造函数中的参数类型变量传递给 对象类型的变量 就会触发隐式构造**

    **类定义:**
    ![](/assets/Snip20190215_1.png)

- **2> 以下4种情况下, 系统会(会触发 隐式构造) 隐式构造一个新对象**
![](/assets/Snip20190215_2.png)























<br>
**3、禁用 隐士构造行为**
**使用 `explicit` 关键字, 修饰单参数构造函数, 可以禁用隐式构造行为, 如下:**

```
class Person{
    int m_age; 
public:
    Person(): m_age(0){
        cout << "Person()" << endl;
    }
    
    // 使用explicit 修饰的单参数构造函数, 禁用隐士构造对象
    explicit Person(int age) : m_age(age) {
        cout << "Person(int age)" << endl;
    }
    
    Person (const Person &pson): m_age(pson.m_age){
        cout << "Person (const Person &pson)" << endl;
    }
    
    ~Person(){
        cout << "~Person()" << endl;
    }
    
    void display(){
        cout << "age: " << m_age << ", Address: " << this << endl;
    }
};


Person p = 20; // 不再被允许, 因为有explicit 修饰
```

<br>
**4、 关于单参数函数的说明**
```
以下3个函数都可以 看成单参数函数
void display(int age = 0 , int price = 0) ; 
void display(int age , int price = 0) ; 
void display(int age) ; 
```
**结论:
    只要可以传一个参数调用的函数,都可以看做单参数函数**

