#### 拷贝构造函数
40:00



<br>
#### 一、构造函数的常识
- 一般来说, 构造函数被调用了,就会有新的对象创建
- 在C++ 中, 有2种构造函数, 普通构造函数和拷贝构造函数

```
class Person{
    int m_age;
    int m_price;
public:
    // 普通构造函数 函数名与每名相同
    Person(int age, int price) : m_age(age), m_price(price){
        cout << "普通构造函数" << endl;
    }
    
    // 拷贝构造函数
    Person(const Person &pson) : m_age(pson.m_age), m_price(pson.m_price){
        cout << "拷贝构造函数" << endl;
    }
    
    ~Person(){
        cout << "析构函数" << end了;
    }
    
};
```