#### 匿名对象(临时对象)

** 1.什么是匿名对象?**
 匿名对象,就是没有被任何变量名或者指针指向的对象用完即销毁.
 
** 2. 如何产生一个匿名对象?**
 直接给构造函数传参,就会产生一个匿名构造函数.(有点像是在类外面调用构造函数, 但是不是调用类的构造函数)
```

 Person pson; // 产生一个栈对象
 Person *p = new Person(); // 产生一个堆对象

 // 以下2行是匿名对象
 Person(10); // 产生一个匿名对象
 Person(); // 产生一个匿名对象
```
 
** 3. 匿名对象的特点**
我们知道, 当对象作为函数的参数 或者 对象作为函数的返回值时, 系统会自动调用拷贝构造函数产生一个临时对象, 而当我们将一个匿名的对象作为函数的实参传给函数时或者将一个匿名对象作为一个函数的返回值时, 系统就不会再调用拷贝构造函数产生一个临时的中间对象了, 这就是匿名对象的 意义所在
 
** 4. 匿名对象, 也是对象,具有对象的所有特质**


**5 匿名对象 示例代码**

```
#include <iostream>
using namespace std;




class Person{
    int m_age;
public:
    Person(int age = 0): m_age(age){
        cout << " 构造 Person(int age )" << endl;
    }
    
    Person(const Person &pson): m_age(pson.m_age){
        cout << " 拷贝构造 Person(const Person &pson) "<< endl;
    }
    ~Person(){
        cout << " 析构 ~Person()" << endl;
    }
    
    void display(){
        cout << "age: " << this->m_age << endl;
    }
};



// 可能产生临时 对象
void displayPerson(Person pson){
    
}

// 可能产生临时 对象
Person testPerson(){
    Person pson(20);
    return pson;
}

//直接返回匿名对象, 不会产生中间对象
Person testNiMing(){
    
    return Person(30);
}

int main(int argc, const char * argv[]) {
   
    
    {
        cout << "--匿名构造函数-------" << endl;
        // 下面2中情况都会产生一个匿名对象
        // 匿名对象有点像在调用 类的构造函数, 但是不是调用类的构造函数
        Person(20);
        Person();
        cout << "---------" << endl;
    }
    
    
    {
        cout << "----可能产生临时对象-----" << endl;
        Person pson;
        displayPerson(pson);
        
        Person ps = testPerson();
        cout << "---------" << endl;
    }
   
    

    {
        cout << "---- 不会 产生临时对象-----" << endl;
        
        displayPerson(Person(10)); // 匿名对象作为函数的实参传入, 不会产生临时对象
        
        Person ps2 = testNiMing(); // 函数直接返回匿名对象, 不会产生 临时对象
        cout << "---------" << endl;
    }

    getchar();
    return 0;
}

```