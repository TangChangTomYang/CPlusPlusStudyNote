#### 域运算符 和 命名空间/

**::** 在C++中的书写位置不同,其表达的含义也不同

<br>
#### 一 **域运算符**

```
// 在.hpp 文件中 声明一个People类
class People {
    int m_age; 
    
public:
    People();
    ~People();
    
    int age();
    void setAge(int age); 
};


// .cpp 文件, 实现类的声明
People::People(){ // 此处表示的是域运算, 是实现People 类中的方法的含义
    cout << "People::People()" << endl;
}
People::~People(){
    cout << "People::~People()" << endl;
}

int People::age(){
    cout << "int People::age()" << endl;
    return this -> m_age;
}
void People::setAge(int age){
    cout << "void People::setAge(int age)" << endl;
    this -> m_age = age;
}

```


<br>
此种情况下(调用函数/访问变量)时, 表示的是 命名空间的含义
```
YR::display(); // 表示的是命名空间的含义
YR::g_age = 20;
```