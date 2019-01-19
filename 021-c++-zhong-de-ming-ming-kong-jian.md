#### C++ 中的命名空间

命名空间可以有效的避免命名冲突, 比如: 在张三和李四正在完成共同的一个项目, 这时,张三和李四 就有可能在定义出 同样名字的类/ 或者函数, 系统就可能冲突, 因此就引出了命名空间的概念.




<br>
#### 一、命名空间的使用情景1
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

namespace YR { // 定义一个叫 YR 的命名空间
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



1:00



<br>
#### 二、命名空间的使用情景2
