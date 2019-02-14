#### 拷贝构造函数

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
 
 
 
 
 <br>
#### 三、 只有基本数据类型成员变量的拷贝构造函数可以不用写(使用系统默认的即可)

```
class Person{
    int m_age;
public:
    Person(int age): m_age(age){
        cout << "普通构造函数 Person(int age)"<< endl;
    }
    
    // 只有基本数据类型的成员变量, 系统实现的拷贝构造函数,就是下面这样,值拷贝(浅拷贝) 没有堆空间的分配, 可以不写
    Person(const Person *pson): m_age(pson.m_age){
        cout << "拷贝构造函数 Person(const Person *pson)" << endl;
    }
    
    
    ~Person(){
        cout << "析构函数" << endl
    }
}

```





<br>
#### 四、C++ / C语言中字符串 拷贝存在的意义 (野指针)

```
class Car {
    int m_price;
    const char *m_name;
public:
    
    // 这个构造函数, 貌似没有问题, 其实问题大了去了
    Car (int price,const char *name ) : m_price(price),m_name(name) {
        
    }
    
    void display(){
        cout << "price:" <<  m_price << "\n" << "name: " << m_name << endl;
    }
};

int main() {
    
    char name[] = {'b','m','w','\0'};
    
    Car *myCar = new Car(100, name);
    myCar->display();
    // 这个代码从语法角度 和 运行情况来看,貌似没有问题, 其实问题大了去了
    // 主要问题如下:
    // 1> name 指向的是一个栈空间的字符数组(字符串), 一旦函数或作用于结束,栈空间自动回收
    // 2> myCar 指向的是一个堆空间, 堆空间不会自动回收, 需要程序员手动回收
    // 3> 堆空间的对象myCar 的成员变量m_name指向的是一个栈空间
    // 4> 后果栈空间(name)先释放, 堆空间(myCar)后释,  通过堆空间(myCar)的成员变量去访问已经释放的栈空间容易造成野指针
    getchar();
    return 0;
}

```
图解如下

![](/assets/Snip20190214_1.png)

比如这样就很危险了
```

Car *myCar(){
    char name[] = {'b','m','w','\0'};
    
    Car *myCar = new Car(100, name);
    return  myCar; // 当其他地方使用myCar就很危险了name已经回收了
}

```


