#### 隐式构造

**1、C++ 中存在隐式构造的现象, 在某些情况下,会隐式调用单参数的构造函数.**

**2、在一下4种情况下, 系统会 隐式构造函数一个新对象**

- **类定义:**
![](/assets/Snip20190215_1.png)

- **以下会触发 隐式构造 对象**
![](/assets/Snip20190215_2.png)


**3、如果不希望系统 隐士构造函数 新对象, 可以在单参数构造函数前加 explicit 修饰,如下:**

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

**4、 关于单参数函数的说明**
```
以下2个函数都可以成为单参数函数
void display(int age , int price = 0) ; 
void display(int age) ; 
```

