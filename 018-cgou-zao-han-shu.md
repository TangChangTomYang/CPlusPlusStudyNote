#### 构造函数





<br>
#### 一、C++ 构造函数


**构造函数(也叫构造器), 在对象创建的时候自动调用, 一般用于完成对象的初始化.**

**特点:**
☆1> 构造函数名必须与类名相同.
☆2> 构造函数无返回值 (返回值类型 void 也不能写, 必须省略)
☆3> 构造函数可以有参数
☆4> 构造函数可以重载, 可以有多个构造函数.
☆☆5> 一旦自定义了构造函数, 必须用其中一个自定义的构造函数来初始化对象

**注意:**
通过malloc 分配的对象不会调用构造函数


**补充:**
1> new/delete 和 malloc/ free 是和堆空间的内管管理相关的,如果和多空间扯不上关系,那么和new/delete/malloc/free 也扯不上关系



<br>
#### 二、 C++ 构造函数在以下几种情况下会被自动调用

```
#include <iostream>
using namespace std;

struct Person{
    int m_age;
    double m_height;
    
    Person(){
        cout << "Person()" << endl;
    }
    
    Person(int age, double height){
        m_age  = age;
        m_height = height;
        cout << "Person(int age, double height)" << endl;
    }
};

// 全局区 对象, 自动调用
Person g_pson; // 全局区的对象,会调用默认的构造函数, 千万不要写成 'Person g_pson()',  'Person g_pson()' 是函数声明而不是全局对象;
Person g_pson2(18,1.67); // 全局区的对象,会调用有参的构造函数
int main (){

    // 栈空间 对象 自动调用
    Person pson; // 千万不要写成功'Person pson()`,'Person pson()` 是函数声明 ;
    pson.m_age = 20;
    pson.m_height = 1.88;
    
    // 栈空间 对象 自动调用
    Person pson1(16,1.88);
    pson1.m_age = 20;
    pson1.m_height = 1.88;

    // 堆空间 对象 自动调用
    // new Person(); 这部分返回的是一个地址,因此只能使用一个指针来存储
    Person *pson2 = new Person();
    pson2 -> m_age = 20;
    pson2 -> m_height = 1.33;
    delete pson2;

    getchar();
    return 0;
}
```


#### 下面是一个经典的案例:

写在全局区和栈区对象时,要谨慎, 不要写成函数声明了, 以下的 对象声明和函数声明容易搞错
![](/assets/Snip20190118_3.png)






<br>
#### 三、通过malloc 分配的对象不会调用构造函数

```
#include <iostream>
using namespace std;

struct Person{
    int m_age;
    double m_height;
    
    Person(){
        cout << "Person()" << endl;
    }
    
    Person(int age, double height){
        m_age  = age;
        m_height = height;
        cout << "Person(int age, double height)" << endl;
    }
}; 

int main (){
    // 通过 malloc 分配的对象不会调动 构造函数
    Person *pson = (Person *)malloc(sizeof(Person));  
    free(pson);
    
    getchar();
    return 0;
}
```


<br>
#### 四、一旦自定义了构造函数, 必须用其中一个自定义的构造函数来初始化对象

```
#include <iostream>
using namespace std;

struct Person{
    int m_age;
    double m_height;
    
    //构造函数 必须与类名相同,没有返回值  
    Person(int age, double height){
         m_age = age;
         m_height = height;
         cout << "Person(int age)" << m_age << endl;
    }
};


int main (){
    
    // 一旦自定义了构造函数, 就必须使用自定义的构造函数初始化对象
//    Person pson1; // 错误, 没有使用自定义构造函数初始化对象
    
    
    Person pson2(19,1.75);  // 使用自定义构造函数初始化对象 ok
    Person *pson3 = new  Person(18,1.75);
    delete pson3;
    
    getchar();
    return 0;
}
```




<br>
#### 五、默认情况下(没有自定义构造函数), 成员变量的初始化情况如下:

![](/assets/Snip20190118_4.png)

如果自定义了构造函数,而没有在构造函数内初始化成员变量, 那么除了全局区的对象, 其他内存空间的成员变量都不会初始化, 需要程序员自己初始化.

也就是说: 只要自定义了构造函数,那么除了全局区的对象,其它区的对象都需要程序员自己初始化.xs

