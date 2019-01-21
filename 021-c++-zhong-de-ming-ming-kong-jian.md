#### C++ 中的命名空间

命名空间可以有效的避免命名冲突, 比如: 在张三和李四正在完同一个项目, 这时,张三和李四 就有可能在定义出 同样名字的类/ 或者函数, 系统就可能冲突, 因此就引出了命名空间的概念.




<br>
#### 一、命名空间的使用情景
```
#include <iostream>
using namespace std; // 这一句表示, 从此行开始,如果没有明确的说明 后面都使用 std 这个命名空间


int g_no; // 这个是全局变量
class Student { // 默认就是无名命名空间(::) 
public:
    int m_age;
     Student(){
        cout << "std::Student()" << endl;
     }
};

namespace YR { // 定义(声明)一个叫 YR 的命名空间
    int g_no; // 这个是全局变量 (是YR命名空间的全局变量)
    class Student {
    public:
        int m_height;
        Student(){
            cout << "YR::Student()" << endl;
        }
    };
}

int main( ) {
    
    // 使用的是 标准命名空间的Student 类
    Student *stu1 = new Student(); // 等价于(无名命名空间(::)) ::Student *stu1 = new ::Student();
    stu1 -> m_age = 10;
    
    
    // 指定 命名空间
    YR::Student *stu2 = new YR::Student();
    stu2 -> m_height = 1.88;
    
    return 0;
}
```






<br>
#### 二、命名空间可能 造成函数调用的二义性

```
// YR 命名空间
namespace YR{
    int g_age;
    void display(){
        cout << "YR::g_age =" << g_age << endl;
    }
}


// FX 命名空间
namespace FX{
    int g_age;
    void display(){
        cout << "FX::g_age =" << g_age << endl;
    }
}


int main(){
    using namsspace YR;
    using namespace FX;
    
    // 下面这2句代码有命名空间的二义性
    // g_age = 20;
    // display();
    
    // 正确的做法
    YR::g_age = 20;
    YR::display();
    // 或者
    FX::g_age = 30;
    FX::display();
}

```








<br>
#### 三、命名空间的嵌套

```
namespace aa{
    int g_age ;
    namespace bb{
        int a_age;
    }
}

int main(){
    aa::bb::g_age = 30;
    return 0;
}

```

全局的命名空间(无名命名空间 ::),所有的命名空间默认情况下都嵌套在它里面

```
int g_age;

namespace aa{
    namespace bb{
        int g_age;
    }
}

int main(){
    g_age = 20; // 等价于 ::g_age = 20;
    
    ::aa::bb::g_age = 30;
    return 0;
}

```

    







<br>
#### 四、命名空间的 合并

以下2种写法是等价的

写法1:
```
namespace aa{
    int g_age;
}

...

namespace aa{
    double g_height;
}
```
等价于
写法2:
```
namespace aa{
    int g_age;
    double g_height;
}
```




<br>
#### 五、声明 和 实现分离, 命名空间的合并

```
// .hpp文件 类的声明
namespace aa{
    class Person{
        int m_age;
        public:
        Person();
        ~Person();
    };
}

// .cpp 文件 类的实现
namespace aa{
    Person::Person(){ // ::表示的是 域运算符 含义
        cout << "Person()" << endl;
    }
        
    Person::~Person(){ // ::表示的是 域运算符 含义
        cout << "Person()" << endl;
    }
}
```








<br>
#### 六、其他编程语言的命名空间

1、 java 中的命名空间 **Pacakage**, 采用的是文件夹分割的概念.

比如: **com** 文件夹中有, **YR**文件夹和 **FX**文件夹, **YR**文件和**FX**文件夹中分别有个同名的**Person.java** 文件, 即有: 
com/YR/Person.java 和 com/FX/Person.java 2个wen件.

那么, 我们在java中应该这样来访问:
```
Package com.YR;
Person *p1 = new Person();

或者
Package com.FX;
Person *p2 = new Person();



```
