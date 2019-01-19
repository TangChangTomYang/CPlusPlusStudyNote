#### 域运算符(::) 和 命名空间(::)

<br>
在C++中, `::` 使用的位置不同, 其含义也是不同的.

<br>
**当我们在实现函数的前面加上 `::` 时, 其表示的是域运算符的含义,如下:**

```
// .hpp 文件,类的声明
class Person{
    int m_age;
    public:
    Person();
    ~Person();
    int age();
    void setAge(int age);
}

// .cpp 文件, 类的实现
// 构造函数的实现
Person::Person(){  // :: 是 域运算付, 限定为 Person类的方法
    cout << "Person::Person()" << endl;
}

// 析构函数的实现
Person::~Person(){ // :: 是 域运算付, 限定为 Person类的方法
    cout << "Person::~Person()" << endl;
}

int Person::age(){
    return m_age;
}

void Person::setAge(int age){
    m_age = age;
}
```





<br>
**当我们在调用函数或调用变量的前面加上 `::` 时, 其表示的是命名空间的含义,如下:**

```
YR::display(); // 表示的是调用 YR 命名空间下的 display 函数
YR::g_age = 20; // 表示访问 YR 命名空间下的 g_age 变量
```


**注意:**
千万不要将 :: 的含义理解错, 



