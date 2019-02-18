#### 运算符重载(String)


<br>
**String.chh 文件**
```
#ifndef String_hpp
#define String_hpp

#include <iostream>
using namespace std;

class String{
    friend ostream &operator<<(ostream &cout, const String &str);
    char *m_cstring = NULL; // Xcode C++ char* 成员变量有个特点, 默认会置为 "", 没搞懂
public:
    String(const char *csting);
    String(const String &str);
    ~String();
    
    // ="cstring" 运算符重载
    String &operator=(const char *cstring);
    // = String 运算符重载
    String &operator=(const String &str);
private:
    String &assign(const char *cstring);
};


// 重载String 的 << 运算符
ostream &operator<<(ostream &cout, const String &str);
#endif /* String_hpp */
```


<br>
**String.cpp 文件**

```
#include "String.hpp"


String::String(const char *cstring){
    assign(cstring);
}

String::String(const String &str){
    assign(str.m_cstring);
}

String::~String(){
    assign(NULL);
}


// ="cstring" 运算符重载
String &String::operator=(const char *cstring){
    return  assign(cstring);
}
// = String 运算符重载
String &String::operator=(const String &str){
    return  assign(str.m_cstring);
}




// 私有方法
String &String::assign(const char *cstring){

    // 避免出现 将同一个堆空间 赋值给自己
    if (this->m_cstring == cstring) return *this;
    
    // 释放旧的堆空间
    if(this->m_cstring){
        cout << "delete 堆空间: " << this->m_cstring << endl;
        delete[] this->m_cstring ;
        this->m_cstring = NULL ;
    }
    
    // 拷贝新的堆空间
    if(cstring){
        cout << "new 堆空间: " << cstring << endl;
        this->m_cstring = new char[strlen(cstring) + 1]{};
        strcpy(this->m_cstring, cstring);
    }
    
    return *this;
}




// 重载String 的 << 运算符
ostream &operator<<(ostream &cout, const String &str){
    if(str.m_cstring == NULL ) return cout;
    return cout << str.m_cstring ;
}
```



**main.mm文件**

```
#include <iostream>
using namespace std;
#include "String.hpp"



int main( ) {

    
    {
        //隐士构造 会调用单参数构造函数
        String name1 = "zhangsan";
        
        //拷贝构造, 需要重写,否则造成二次 释放堆空间
        String name2 = name1;
        
        //重载字符串,赋值运算符, 否则堆空间会被重复释放2次
        name2 = "lisi";
 
        String name3 = "wangwu";
        // 重写String 赋值运算符 =, 否则造成 name2 堆空间2次释放
        name3 = name2;
        
        
        cout << name3 << endl;
        
        cout << name1 <<  "\n" << name2 << endl;
        // 内存管理, 一个new 对应一个delete
        String *account = new String("123456");
        cout << account << endl;
        delete  account;
        
    }
   
    
    getchar();
    return 0;
}
```
