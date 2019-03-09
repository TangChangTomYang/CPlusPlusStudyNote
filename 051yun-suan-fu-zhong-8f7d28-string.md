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
    friend bool operator>(const char *cstring1, const String &str);
    
    // 赋值为NULL是安全处理
    char *m_cstring = NULL; // Xcode C++ char* 成员变量有个特点, 默认会置为 ""
public:
    /******构造函数**********************************/
    String(const char *csting = "");
    /******拷贝构造函数**********************************/
    String(const String &str);
    /******析构函数**********************************/
    ~String();
    
    
    unsigned long length();
    
    /******运算符重载函数**********************************/
    // ="cstring" 运算符重载(避免产生 String str = "abc"; 时产生隐式构造)
    String &operator=(const char *cstring);
    // = String 运算符重载
    String &operator=(const String &str);
    
    // +"cstring" 运算符重载
    String operator+(const char *cstring);
    // +String 运算符重载
    String operator+(const String &str);
    
    // +="cstring" 运算符重载
    String &operator+=(const char *cstring);
    // +="String" 运算符重载
    String &operator+=(const String &str);
    // [] 运算符重载, str[1]
    char operator[](long index);
    // >"cstring" 运算符重载
    bool operator>(const char *cstring);
    // >"String" 运算符重载
    bool operator>(const String &str);
    
    
private:
    /******私有成员函数**********************************/
    String &assign(const char *cstring);
    char *join(const char *cstring1, const char *cstring2);
};

/******全局函数**********************************/
// 重载String 的 << 运算符
ostream &operator<<(ostream &cout, const String &str);
// 重载char* > String的 > 运算符
bool operator>(const char *cstring1, const String &str);
#endif /* String_hpp */

```


<br>
**String.cpp 文件**

```
#include "String.hpp"

/******构造函数**********************************/
String::String(const char *cstring){
    assign(cstring);
}

/******拷贝构造函数**********************************/
String::String(const String &str){
    assign(str.m_cstring);
}

/******析构函数**********************************/
String::~String(){
    assign(NULL);
}


/******(一般)成员函数**********************************/
unsigned long String::length(){
    if (this->m_cstring == NULL ) return 0;
    return strlen(this->m_cstring);
}

/******运算符重载函数**********************************/
// ="cstring" 运算符重载
String &String::operator=(const char *cstring){
    return  assign(cstring);
}
// = String 运算符重载
String &String::operator=(const String &str){
    return  assign(str.m_cstring);
}

// +"cstring" 运算符重载
String String::operator+(const char *cstring){
    String  str; // 这里是创建对象而非 声明变量
    char *newcstring = join(this->m_cstring, cstring);
    if (newcstring != NULL){
        // 释放旧的cstring (因为Stirng 对象最少都有一个堆空间字符串  "" )
        str.assign(NULL );
        str.m_cstring = newcstring; // newcstring 已经是一个新鲜的了, 直接指向即可
        
    }
    return  str;
}
// +String 运算符重载
String String::operator+(const String &str){
    return operator+(str.m_cstring);
}

// +="cstring" 运算符重载
String &String::operator+=(const char *cstring){
    char *newcstring = join(this->m_cstring, cstring);
    if (newcstring != NULL ) {
        assign(NULL);
        this->m_cstring = newcstring;
        
        // 注意这里不能直接 assign(newcstring); // 会造成newcstring 无法释放
    }
    return *this;
}
// +="String" 运算符重载
String &String::operator+=(const String &str){
    return operator+=(str.m_cstring);
}

// [] 运算符重载, str[1]
char String::operator[](long index){
    if(index < 0 || index >= this->length() || this->m_cstring == NULL ) return '\0';
    return (this->m_cstring)[index];
}



// >"cstring" 运算符重载
bool String::operator>(const char *cstring){
    //  rst > 0 str1 > str2, rst == 0 相等, rst < 0 str1 < str2
    if (this->m_cstring == NULL && cstring == NULL ) return 0;
    return (strcmp(this->m_cstring, cstring) > 0);
    
}
// >"String" 运算符重载
bool String::operator>(const String &str){
    
    return operator>(str.m_cstring);
}

/******私有成员函数**********************************/
// 私有方法
String &String::assign(const char *cstring){

    // 避免出现 将同一个堆空间 赋值给自己
    if (this->m_cstring == cstring) return *this;
    
    // 释放旧的堆空间
    if(this->m_cstring){
        cout << "delete 堆空间: " << this->m_cstring << endl;
        // 释放旧指针空间
        delete[] this->m_cstring ;
        // 清空明原有字符串指针
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

char *String::join(const char *cstring1, const char *cstring2){
    
    if(cstring1 == NULL || cstring2 == NULL) return NULL ;
    
    char *newcstring = new char[strlen(cstring1) + strlen(cstring2) + 1]{};
    strcat(newcstring, cstring1);
    strcat(newcstring, cstring2);
    cout << "join new 新 堆空间: " << newcstring << endl;
    return newcstring;
}



/******全局函数**********************************/
// 重载String 的 << 运算符
ostream &operator<<(ostream &cout, const String &str){
    if(str.m_cstring == NULL ) return cout;
    return cout << str.m_cstring ; //cout 调用完毕会返回一个cout对象(ostream 对象)
}

// 重载char* > String的 > 运算符
bool operator>(const char *cstring, const String &str){
    //  rst > 0 str1 > str2, rst == 0 相等, rst < 0 str1 < str2
    if (str.m_cstring == NULL && cstring == NULL ) return 0;
    return (strcmp( cstring, str.m_cstring) > 0);
}
```
