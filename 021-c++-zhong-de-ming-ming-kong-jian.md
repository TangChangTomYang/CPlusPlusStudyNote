#### C++ 中的命名空间

命名空间可以有效的避免命名冲突


<br>
#### 一 命名空间的使用情景1
```
#include <iostream>
using namespace std;

/** 命名空间可以避免 命名冲突
 */

// 使用情景1:
// 在不同的命令空间,定义相同名字的类
class Student {
public:
    int m_age;
};

namespace YR { // 定义一个叫 YR 的命名空间
    class Student {
    public:
        int m_height;
    };
}

int main( ) {
    
    // 使用的是 标准命名空间的Student 类
    Student *stu1 = new Student();
    stu1 -> m_age = 10;
    
    
    // 指定 命名空间
    YR::Student *stu2 = new YR::Student();
    stu2 -> m_height = 1.88;
    
    return 0;
}
```