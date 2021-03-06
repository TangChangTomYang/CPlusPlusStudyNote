#### const   常亮

#### 一、const 特点概述



<br>
#### 二、const 示例
1、**const 是常量的意思, 被其修饰的变量是不可修改的.**

![](/assets/Snip20190113_6.png)


<br>
2、**consts 常量在初始化时必须赋值**

![](/assets/Snip20190113_7.png)


<br>
3、**const** 修饰的 **类/ 结构体 **, 其成员也是不可以修改的.

![](/assets/Snip20190113_8.png)


<br>
4、**const 修饰的 对象/结构体 /对象的指针/ 结构体指针, 其成员也是不可以修改的.**
![](/assets/Snip20190113_9.png)




<br>
#### 二、const 面试题
**1、面试题1**
![](/assets/Snip20190113_10.png)

**2、面试题2**
const 修饰的结构体/ 类/ 结构体指针/ 类指针,不论是指针还是里面的成员变量都不能改.


<br>
#### 三、常引用(比如: int const &rAge = age)的特点
**1、 常引用指向的内容的值是不能修改的**
![](/assets/Snip20190113_11.png)




<br>
**2、 常引用可以指向常亮**
```
int age = 10;
int &rAge = age; 

int &rAge1 = 10;// 错误, 引用不能指向常亮.
int const &rAge2 = 20; // 常引用可以指向常亮
```



<br>
**3、 常引用可指向表达式**
```
int a = 10;
int b = 20;
int &rAge =  a + b ; // 引用不能指向表达式
int const &rAge1 = a + b ;// 常引用可以指向表达式
```





<br>
**4、 常引用可以指向不同的数据类型**
```
int age = 20;
double &rAge = age; // 将4个字节的数据存在8个字节中,不允许
double const &rAge2 = age ; // 常引用可以存储不同的数据类型的值
```

<br>
**5、const 引用 作为参数的特点(可以接收 const 和 非const的实参)**
![](/assets/Snip20190113_12.png)



<br>
**6、const 的引用作为函数参数可以和非const 的引用作为参数 构成重载, 此规则也使用与指针**
 ![](/assets/Snip20190113_13.png)
 
 
 <br>
 **7、当字符串作为函数参数时, 最好定义为 const char * 类型, 这样 兼容性好**
![](/assets/Snip20190218_2.png)



<br>
**☆☆☆☆☆8、const 对象/ const 引用 不能调用非const 函数**


<br>

#### 四、 常引用指向不同类型的数据的特点

**当常引用指向了不同类型的数据时,会产生临时变量,即引用指向的并不是初始化指向的那个变量.** 这是C++ 为了数据安全考虑

![](/assets/Snip20190115_1.png)









<br>

#### 五、 引用的本质 
1> 引用的本质就是指针.
2> 只是引用在初始化时就必须赋值
3> 引用一旦赋值指向了一个变量就不能再指向其它变量了.





















