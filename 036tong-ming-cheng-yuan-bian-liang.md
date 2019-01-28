#### 同名成员变零

所谓同名成员变量,就是指的是,父类和子类有相同的成员变量,如下:

```
class Student{
public:
    int m_age;
};

class Worker{
public:

    int m_age;
};

class Undergraduate : public Student, public Worker{
public:
    int m_age;
};


同名的成员变量和同名的函数一样, 我们也是通过 域运算符来做限定调用的.

Undergraduate *ug = new Undergraduate();

// 通过域 运算符做限定
ug->m_age = 10;
ug->Student::m_age = 10;
ug->Worker::m_age = 10;

cout << ug->m_age << endl;
cout << ug->Student::m_age << endl;
cout << ug->Worker::m_age << endl;


```

**说明:**

父类/子类虽然有相同的成员变量, 但是在内存中是各自占用各自的位置,不会相互覆盖的

![](/assets/Snip20190129_1.png)