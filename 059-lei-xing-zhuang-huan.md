#### 类型转换


**1、C语言风格的类型转换符(2种类型)**
```
// 类型1, 在C语言中和C++语言中都可以这样写
(type) expression
// 类型2, 在C++ 语言中还可以这样写
type(expression)

eg:
int a = 0;
double b1 = (double)a; // C语言风格类型转换
double b2 = double(a); // C语言风格类型转换, C++ 中可以这么写
```

<br>
**2、C++ 中有4个类型转换符**
- static_cast
- dynamic_cast
- reinterpret_cast
- const_cast

**使用格式: xxx_cast<type>(expression)**

**说明: 
一般C++ 中的4个类型转换符(static_cast/ dynamic_cast/ reinterpret_cast/ const_cast) 是用于C++ 的类对象的转换, 而 C 语言风格的类型转换一般是用于基本数据类型的转换**



<br>
<br>
<br>

```
class Person{
public:
    int m_age;
    Person(int  age):m_age(age){
        
    }
};
```

**3、const_cast 类型转换**
**一般用于去除 const 属性, 将const转换成非const, 更专业**

```
// const_cast 将const 强制转换陈 非 const
void testConstCast(){
    // const_cast, 将const的对象转换成非const 的对象
    const Person *p1 = new Person(10);
    // p1->m_age = 30; const 对象是不能被修改的
    cout << "p1->m_age: " << p1->m_age<< endl;
    
    // Person *p2 = p1;  非const 对象指针是不能直接指向 const 对象指针的
    Person *p2 = const_cast<Person *>(p1); // const_cast可以将const 强制转换成非const
    p2->m_age = 40;
    cout << "p2->m_age: " << p2->m_age<< endl;
    
    //(Person *)p1 与 const_cast<Person *>(p1) 等价, 只是看起来更专业些
    Person *p3 = (Person *)p1;
    p3->m_age = 50;
    cout << "p3->m_age: " << p3->m_age<< endl;
}
```


<br>
**4、dynamic_cast**
**一般用于多态类型的转换, 有运行时安全监测, 更安全**

```
class Person{
public:
    int m_age;
    Person(int  age):m_age(age){
        
    }
    virtual void run(){
        
    }
    
    ~Person(){}
};

class Student : public Person{
public:
    Student(int age): Person(age){
        
    }
};

class Car{
    
};

// 一般用于多态类型的转换, 有运行时安全监测
// dynamic_cast<Student *>(p1) 相较于 (Student *)p1 更安全, 不会出现野指针错误
void testDynamicCast(){
    
    Person *p1 = new Person(10);
    Person *p2 = new Student(20);
    

    Student *stu1 = dynamic_cast<Student *>(p1); // NULL
    Student *stu2 = dynamic_cast<Student *>(p2);
    Car *car = dynamic_cast<Car *>(p1); // NULL
}
```

**注意:**
**dynamic_cast<type >(expression); 中的对象,必须有多态, 否则不能使用 dynamic_cast 类型转换**

<br>
**5、 static_cast**
- 对比 dynamic_cast ,static_cast 缺乏运行时安全检测.
- 不能交叉转换(不是同一继承体系的, 无法转换)
- 常用于基本数据类型的转换, 常用于非const 转换成const
```
// static_cast 和 dynamic_cast 差不多
// static_cast 内有dynamic_cast运行时动态检测, 数据不安全
// static 只能用于同一继承体系下的 转换
void testStaticcast(){
    
    Person *p1 = new Person(10);
    Person *p2 = new Student(20);
    
    Student *stu1 = static_cast<Student *>(p1); // 不安全
    Student *stu2 = static_cast<Student *>(p2);
//    Car *car = static_cast<Car *>(p1); // 只有同一继承体系才可以
    
    // 常用于基本数据类型的转换 和 非const 转成const
    int a = 0;
    double b = static_cast<double>(a);
    const Person *p3 = static_cast<Person *>(p1);
}
```




<br>
**6、 reinterpret_cast**

**1> 属于比较底层的强制转换,没有任何类型检查和格式转换, 仅仅是简单的二进制数据拷贝**
**2> 可以交叉转换**


