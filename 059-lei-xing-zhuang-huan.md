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
**一般用于去除 const 属性, 将const转换成非const**

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



