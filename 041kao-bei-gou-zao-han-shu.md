#### 拷贝构造函数
40:00



<br>
#### 一、构造函数的常识
- 一般来说, 构造函数被调用了,就会有新的对象创建
- 在C++ 中, 有2种构造函数, **普通构造函数和拷贝构造函数**

```
class Person{
    int m_age;
    int m_price;
public:
    // 普通构造函数 函数名与每名相同
    Person(int age, int price) : m_age(age), m_price(price){
        cout << "普通构造函数" << endl;
    }
    
    // 拷贝构造函数 (拷贝构造函数有且接收一个 const 类型的引用)
    Person(const Person &pson) : m_age(pson.m_age), m_price(pson.m_price){
        cout << "拷贝构造函数" << endl;
    }
    
    ~Person(){
        cout << "析构函数" << end了;
    }
    
};
```



<br>
#### 二、子类构造函数调用父类构造函数, 子类拷贝构造函数调用父类拷贝构造函数

```
class Person{
    int m_age;
public:
    // 构造函数
    Person(int age) : m_age(age){
        cout << "父类构造函数调用 Person(int age) " << endl;
    }
    
    // 拷贝构造函数, 有且仅接收一个const 的引用
    Person(const Person &pson){
        cout << "父类 拷贝构造函数调用  Person(const Person &pson)" << endl;
    }
    
    ~Person(){
        cout << "父类析构函数 ~Person()" << endl;
    }
    
};

class Student : public Person{
    int m_score;
public:
    
    // 子类构造函数, 只能在初始化列表调用父类构造函数
    Student(int age , int score): Person(age), m_score(score){
        cout << "子类构造函数调用父类构造函数" << endl;
    }
    
    // 子类 拷贝构造函数, 有且仅接收一个const 的引用, 子类拷贝构造函数只能在初始化列表调用父类的拷贝构造函数
    Student (const Student &stu) : Person(stu) , m_score(stu.m_score){
        cout << "子类的 拷贝构造函数, 自能在初始化列表中调用父类的拷贝构造函数" << end了;
    }
    
    ~Student(){
        cout << "子类析构函数 ~Student() " << endl;
    }
};   

 ``` 
