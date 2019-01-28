#### 同名函数

如果父类, 子类 有相同名字的函数, 我们通过 域运算符来做限定调用, 有点类似于其它语言中 使用 super 来调用父类的方法. 



```
class Student{
public:
    void eat(){
        cout << "void Student::eat()" << endl;
    }
};

class Worker{
public:
    void eat(){
        cout << "void Worker::eat()" << endl;
    }
};

class Undergraduate : public Student, public Worker{
public:
    void eat(){
        cout << "void Undergraduate::eat()" << endl;
    }
};


// 从上面的类的定义来看, 父类 子类都有同名的函数, 那么如果我们想要通过子类的指针来调用父类的方法,C++ 中是通过 域云算符 来做限定的,如下:

Undergraduate *ug = new Undergraduate();
ug->eat();  // 调用Undergraduate自己的函数
ug->Student::eat(); // 调用Undergraduate 父类Student的函数
ug->Worker::eat(); // 调用Undergraduate 父类Worker的函数
```

