#### 一、面向对象的3大特性

**1、封装, 就是成员变量私有化,提供函数接口给外部访问私有化成员变量(封装的好处不止于此)**
**2、继承, 父类的成员变量在前, 子类的成员变量在后**
**3、多态**
- **1> 同一操作,用在不同的对象, 可以有不同的解释,产生不同的执行结果.**
- **2> 在运行时,可以识别出真正的对象类型, 调用对应子类中的方法.**
- **3> C++ 中的多态是通过虚函数(virtual function) 来实现的.**



<br>
#### 二、父类指针 子类指针

**1、父类指针可以指向子类对象,是安全的. 开发中经常用到(继承需要使用public). 其实,父类指针指向子类对象是属于多态的范畴**
**2、子类指针执行父类对象,是不安全的**




<br>
####三、 默认情况下,C++ 中函数调用 和 调用函数的指针类型直接相关, 和指针指向对象类型无关

**1、 默认情况下 C++ 中函数调用, 是根据指针的具体类型来决定的, 与指向的真实对象类型无关, 因此默认情况下C++ 中的函数不存在多态的效果**
```
namespace test1 { // 多态测试1
    
    class Animal {
        int m_age;
    public:
        void  run(){
            cout << "void  Animal::run()"<< endl;
        }
    };
    
    class Cat : public Animal {
        int m_life;
    public:
        void  run(){
            cout << "void  Cat::run()"<< endl;
        }
    };
    
    class Dog : public Animal {
    public:
        void  run(){
            cout << "void  Dog::run()"<< endl;
        }
    };
    
    
    
    void liu(Animal *animal){
        animal -> run(); // 不论,animal 指向的真实对象类型是什么, 都只会调用 Animal 的 run 方法
    }
    
}


测试1:
void testDemo1()  {
    using namespace test1;
    
    Animal *animal = new Animal();
    Cat *cat  = new Cat();
    Dog *dog = new Dog();
    
    // 我们想要的是 ,传入什么参数, 就调用对应动物的 run 方法, 想要达到多态的效果
    liu(animal);
    liu(cat);
    liu(dog);
    
    delete  animal;
    delete cat;
    delete dog;
    
    /*
     打印结果: 失望了 没有多态
     void  Animal::run()
     void  Animal::run()
     void  Animal::run()
     */
    
}



测试2:
void testDemo2(){
    
    using namespace test1;
    // 为什么会这样呢,没有多态的效果呢? 我们来验证一下
    
    cout <<"--------realCat----------------------------" << endl;
    Cat *realCat = new Cat();
    realCat -> run();
    
    cout <<"--------testAnimal----------------------------" << endl;
    Animal *testAnimal  = (Animal  *)realCat;
    testAnimal -> run();
    
    cout <<"--------testCat----------------------------" << endl;
    Cat *testCat = (Cat  *)realCat;
    testCat -> run();
    cout <<"--------testDog----------------------------" << endl;
    Dog *testDog = (Dog  *)realCat;
    testDog -> run();
    
    
    
    /* 打印结果:
     --------realCat----------------------------
     void  Cat::run()
     --------testAnimal----------------------------
     void  Animal::run()
     --------testCat----------------------------
     void  Cat::run()
     --------testDog----------------------------
     void  Dog::run()*/
}
```
**经过测试验证, 我们发现如下的结论:**
- **1> 默认情况下 函数的调用 与 调用它的指针类型直接相关的,指针是什么类型, 就会去调用对应类的对应方法, 而和对象真实类型无关**

**看见这个结论你肯定蒙圈了,乱套了**
- **其实, C++ 就是这样的,C++ 是静态语言, 怎么写,就怎么调用,写了就定了(编译时就定死了)**. 
- **Objective-c  是动态语言, 在执行的时候才会决定怎么做**





<br>
####三、 C++ 中多态的实现

**1、在 C++ 的类中定义函数时, 函数前使用 virtual 修饰为 虚函数, 使用public 方式继承并重写父类虚函数就可以实现多态.
**
1> 只要父类定义了 某一个(xxx函数) 函数为虚函数, 那么 子类中的(xxx函数)都为虚函数.

**2、多态的特点:**
1> 可以使用父类指针指向子类的对象
2> 当使用父类指针指向子类对象后, 通过父类指针调用 虚函数后, 会直接调用真实对象(子类对象)类型的函数.

**3、为了实现多态,子类必须这样做**
1> 使用public 方式继承 父类
2> 重写父类的虚函数
3> 使用父类指针调用虚函数方法

```
namespace DuoTai {
    class Person{
        int  m_age;
    public:
        virtual void run(){ // virtual 定义虚函数实现多态, 一路虚到底,子类必须使用 public 继承,否则就没有多态
            cout << "void Person::run()" << endl;
        }
    };
    
    
    class Student : public Person{ // 必须使用 public 继承
        int m_no;
    public:
        void run(){
            cout << "void Student::run()" << endl;
        }
    };
    
    class GoodStudent : public Person{ // 必须使用 public 继承
        
    public:
        void run(){
            cout << "void GoodStudent::run()" << endl;
        }
    };
    
}

测试:
void testDuoTai(){
    using namespace DuoTai;
    
    Person  *pson1 = new Person;
    Person  *pson2 = new Student;
    Person  *pson3 = new GoodStudent;
    pson1 -> run();
    pson2 -> run();
    pson3 -> run();
    
    
}

结果:
void Person::run()
void Student::run()
void GoodStudent::run()
```




<br>
#### 四、 虚函数

1、C++ 中多态通过虚函数来实现.
2、虚函数, 被virtual 修饰的函数,就是虚函数
3、只要在父类中声明为虚函数,子类中重写的函数也自动变成虚函数(也就是说子类中可以省略virtual 关键字)
4、只要在类中定义过虚函数, 那么当前类及其子类的 每个对象的大小会增大4(或者8)字节来存储当前对象的虚表(即定义过虚函数的对象要比普通函数的对象大4(或者8)字节).
