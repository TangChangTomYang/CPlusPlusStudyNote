#### 拷贝构造函数

<br>
#### 一、构造函数的常识
- **1> 一般来说, 构造函数被调用了,就会有新的对象创建**
- **2> 在C++ 中, 有2种构造函数, `普通构造函数 和 拷贝构造函数`**





<br>
####二、拷贝构造函数

**1、什么是拷贝构造函数?**
** 函数名与类名相同, 有且只有一个当前类 的引用类型参数的函数就是拷贝构造函数(拷贝构造函数和构造函数一样没有返回值),如下:**

```
class Person{
    int m_age;
    int m_price;
public:
    // 普通构造函数 函数名与类名相同
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
#### 三、拷贝构造函数 被调用

**1、将一个对象, 直接赋值给另一个 未初始化的对象类型变量时, 会调用拷贝构造函数, 构造一个新的对象**
```
Person p1("zhangsan");
Person p2 = p1; // 会调用拷贝构造

// 或者
Person *p3 = new Person("lisi");
Person p4 = *p3; // 会调动拷贝构造

```
**这种直接将一个对象直接赋值给另一个未初始化对象, 可以通过运算符重载来规避**



<br>
**2、将一个对象作为 单参数构造函数的参数时 会调用构造函数**
```
Person p1("zhangsan");
Person *p2 = new Person(p1); // 会调用拷贝构造

//或者
Person *p3 = new Person("lisi");
Person p4 = new Person(*p3); // 会调用拷贝构造
```

<br>
**3、将一个对象赋值给另一个对象, 不会调用拷贝构造, 很危险, 容易在成堆空间被多次释放, 必须重载运算符解决**
```
Person p1("zhagnsan");
Person p2("lisi");

//此种情况属于浅拷贝, p1的地址不会变
p1 = p2; 
// 此种情况容易造成 p1 成员指向的堆空间无法释放, p2成员指向的堆空间 被 释放多次, 必须重载 = 运算符

```



<br>
#### 三、子类构造函数调用父类构造函数, 子类拷贝构造函数调用父类拷贝构造函数

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
#### 四、 只有基本数据类型成员变量的拷贝构造函数可以不用写(使用系统默认的即可)

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
#### 五、C++ / C语言中字符串 拷贝存在的意义 (野指针)

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




<br>
#### 六、C++ / C语言中字符串 的正确用法 (拷贝字符串到堆空间,包住它的名)

```
class Che{
    int m_price;
    char *m_name;
public:
    // 构造函数
    Che(int price , const char *name = NULL ) : m_price(price){

        if (name == NULL )  return;
        // 申请堆空间存储字符串
        this-> m_name = new char[strlen(name) + 1]{}; // {}的作用是初始化为 全0
        // 拷贝字符串内容
        strcpy(this-> m_name, name); // char *__dst 表示的是目标字符串,const char *__src 表示的是源字符串
        
        cout << " Che(int price , const char *name = NULL )" << endl;
    }
    
    // 拷贝构造函数
    Che(const Che &che):m_price(che.m_price){
        
        // 拷贝字符串
        if (che.m_name != NULL) {
            // 申请堆空间存储字符串
            this->m_name = new char[strlen(che.m_name) + 1]{}; //  {} 的作用是初始化为 0
            strcpy(this->m_name, che.m_name);
        }
    }
    
    // 析构函数
    ~Che(){
        
        // 释放堆空间, 要写严谨点
        if(this->m_name != NULL) {
            delete[] m_name; // 因为 new 的时候 char[] 有[], delete 时也要带[]
            m_name = NULL; // 清空指针, 方式释放后再次使用造成野指针
        }
        
        cout << "~Che()" << endl;
    }
};
```





<br>
#### 八、 C++ 中的对象拷贝

**1、拷贝构造函数 (copy Constructor)**
-  拷贝构造函数是构造函数的一种
-  当利用已存在的对象,创建一个新的对象时(类似于拷贝), 就会调用新对象的拷贝构造函数进行初始化
-  拷贝构造函数的格式是固定的, 接收一个 const 引用作为参数




**2、 C++对象拷贝示例**
```
class Car{
    int m_price;
public:
    // 构造函数
    Car(int price = 0) : m_price(price){
        
        cout << "Car(int price = 0) " << endl;
    }
    
    //拷贝构造函数, 接收一个 const 引用
//    Car(const Car &car){
//        cout << "Car(const Car &car)" << endl;
//        this->m_price = car.m_price;
//    }
//    拷贝构造函数也可以这样写, 和构造函数一样, 也是可以有初始化列表的
    Car(const Car &car):m_price(car.m_price){ // 其实像这种只包含基本数据类型的拷贝构造函数完全可以不写(默认系统也是这样实现的)
        cout << "Car(const Car &car)" << endl;
    }
    
    
    void display(){
        cout << "price:" << this -> m_price << endl;
        cout << "address: " << this << endl;
    }
};


void testCopyCar(){
    // 利用构造函数创建对象
    Car zCar1(20) ; // 栈对象
    zCar1.display();
    Car *dCar1 = new Car(10); // 堆对象
    dCar1->display();
    cout << endl;
    
    Car zcCar1 = Car(zCar1); // 栈拷贝
    zcCar1.display();
    Car *dcCar1 = new  Car(zCar1); // 堆拷贝
    dcCar1->display();
    cout << endl;
    
    Car zcCar11 = zCar1; // 栈拷贝 等价于  Car zcCar11 = Car(zCar1);
    zcCar11.display();
    
    // 注意下面这种写法不是拷贝, 是赋值
    Car zCar50(50);
    cout << "---zCar50----" << &zCar50 << endl;
    Car zcCar50;
    cout << "---zcCar50----" << &zcCar50 << endl;
    // 注意, 这里不是拷贝操作是赋值操作,是将zCar50 的空间赋值给zcCar50
    // 拷贝是利用一个已经存在的对象产生一个新对象, 而赋值不会产生新对象
    zcCar50 = zCar50;
    cout << "---zcCar50----" << &zcCar50 << endl;
    cout << endl;
    
    Car zcCar2 = Car(*dCar1); // 栈拷贝
    zcCar2.display();
    Car *dcCar2 = new Car(*dCar1); // 堆拷贝
    dcCar2->display();
}

```








<br>
#### 七、浅拷贝 深拷贝
**1、 编译器默认提供的拷贝是浅拷贝(shallow copy)**
- 将一个对象的所有成员变量的值拷贝到另外一个对象
- 如果某个成员变量是指针, 只会拷贝指针中存储的地址值,并不会拷贝指针指向的存储空间
- 浅拷贝可能导致堆空间多次释放 free 的问题.

**2、如果需要实现深拷贝(deep copy), 就需要自定义拷贝构造函数**
- 将指针类型的成员变量所指向的堆空间,也进行一次拷贝(拷贝到新申请的堆空间),而非仅仅拷贝指针的地址值
