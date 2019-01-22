#### C++ 中的初始化列表

<br>
**1、 什么是初始化列表? **
1> 初始化列表是一种便捷的成员变量初始化方式
2> 初始化列表是C++ 的一种特性, C 语言没有这种特性.
3> 初始化列表只能用在C++ 的构造函数中.
如下: 
```
struct Person{
    int m_age;
    double m_height;
    
    //这是一般的构造函数写法
    //Person(int age, double height){
    //    this -> m_age = age;
    //    this -> m_height = height;
    //}
    
    // 使用初始化列表,来初始化构造函数
    Person(int age, double height) : m_age(age), m_height(height){ 
    
    // 上面的 m_age(age) 就相当于 this->m_age = age;// 初识化的值 可以是任何表达式
    }
}

```


<br>
**2、初始化列表的,初始化的顺序只和成员变量的定义顺序有关**
```
struct Person{
    int m_age;
    double m_height;
      
    // 初始化 与 m_age(age)和m_height(height)的书写顺序无关, 是和m_age 与 m_height定义顺序相关
    Person(int age, double height) : m_age(age), m_height(height){ 
    
    // 上面的 m_age(age) 就相当于 this->m_age = age;// 初识化的值 可以是任何表达式
    }
}

```


<br>
**3、如果构造函数既写了初始化列表, 又在构造函数内写了表达式, 那么先执行初始化列表再执行表达式**

```
struct Person{
    int m_age;
    double m_height;
 
    Person(int age, double height) : m_age(age), m_height(height){ 
         this -> m_age = age;
         this -> m_height = height;

    }
    
    //相当于
    //Person(int age, double height) { 
             //m_age(age);
             //m_height(height);
             //this -> m_age = age;
             //this -> m_height = height;
    //}

}

```




<br>
**4、初识化列表只能写在函数的实现部分**

```
// 声明部分
struct Dog{
    int m_age;
    Dog(int age );
}

// 实现部分
Dog::Dog(int age) : m_age(age){ // 初始化列表只能写在函数的实现
    
}

```




