#### C++ 中的对象存储位置


**1、C++ 中的对象(数据结构)可以存在的位置分为3个**
 1> 全局区
 2> 栈空间
 3> 堆空间
 
 **其它,高级语言,比如 Objective-C  对象只能放堆空间.**
 



```
#include <iostream>
using namespace std;
struct Person{
    int m_age;
    int m_height;
};

// 全局区
Person g_pson;
int main (){
    
    // 栈空间
    person pson;
    pson.m_age = 20;
    pson.m_height = 1.88;
    
    // 堆空间
    // new Person(); 这部分返回的是一个地址,因此只能使用一个指针来存储
    Person *pson2 = new Person();
    pson2 -> m_age = 20;
    pson2 -> m_height = 1.33;
    delete pson2;
    
    // 堆空间的对象也可以这样来获取
    Person *pson3 = (Person *)malloc(sizeof(Person)); // c++ 中不推荐这样做
    pson3 -> m_age = 30;
    pson3 -> m_height = 1.43;
    free(pson3);
    
    
    getchar();
    return;
}

```