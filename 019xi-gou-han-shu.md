#### 析构函数 (Destructor)


析构函数(也叫析构器), 在对象销毁的时候自动调用, 一般用于对象的清理工作.

**特点:**
1> 析构函数以波浪线`'~'` 开头, 无返回值, 无参数, 不可以重载, 一个类有且只能有一个析构函数.
2> 析构函数的名字一定要与类名相同, 只是前面多一个波浪线`'~'`.

**注意:**
1> 不能主动调用析构函数, 析构函数是被系统自动调用的.
2> 析构函数和构造函数一样,必须要声明为 **public**, 否则报错,外面不能访问.
3> 使用 **struct** 声明的类,默认权限就是**public**, 因此使用 **struct** 声明的类,因此 构造函数和析构函数可以不用再显示的声明为 **public**.
4> 使用 **Class** 声明的类, 默认情况下成员变量和方法为 **private**, 因此使用 **class** 声明的类需要显示的声明 构造函数和析构函数为 **public** ,否则外部莫法使用这个类.
5> 通过 **malloc** 分配的对象,不会调用构造函数和析构函数


<br>
#### 二、 析构函数的作用

析构函数是用来回收在对象(比如: person 对象)内部申请的堆空间

```
struct Car{
    double m_price;
    Car(){ // 构造函数
        cout << "Car()" << endl;
    }
    ~Car(){ //析构函数
        cout << "~Car()" << endl;
    }
};

class Student{
    int m_age;
    double m_height;
    Car *m_car;
public: // 构造函数和析构函数必须定义为 public
    Student(){
        cout << "Student()" << endl;
        this -> m_car = new Car(); // 对象内部申请一个堆空间
    }
    
    ~Student(){
        cout << "~Student()" << endl;
        delete this -> m_car; // 对象销毁时,必须将在自己内部申请的堆空间回收掉, 这时 析构函数的作用
    }
    
};

void test(){
    Student *stu = new Student();
    delete stu; // new 和 delete 必须成对出现
}

```

