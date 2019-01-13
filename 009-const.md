#### const  

1、**const** 是常量的意思, 被其修饰的变量是不可修改的.

![](/assets/Snip20190113_6.png)

2、**consts** 常亮在初始化时必须赋值

![](/assets/Snip20190113_7.png)

3、**const** 修饰的是 **类/ 结构体 **, 其成员也是不可以修改的.

![](/assets/Snip20190113_8.png)
// 

4、**const** 修饰的是 **类/ 结构体  ** 指针, 其成员也是不可以修改的.
![](/assets/Snip20190113_9.png)




<br>
#### 二、const 面试题
1、面试题1
![](/assets/Snip20190113_10.png)

2、面试题2
const 修饰的结构体/ 类/ 结构体指针/ 类指针,不论是指针还是里面的成员变量都不能改.


<br>

#### 三、常引用的特点
1、 常引用指向的内容的值是不能修改的
![](/assets/Snip20190113_11.png)

2、 常引用可以指向常亮

```
int age = 10;
int &rAge = age; 

int &rAge1 = 10;// 错误, 引用不能指向常亮.
int const &rAge2 = 20; // 常引用可以指向常亮
```

3、 常引用可指向表达式
```
int a = 10;
int b = 20;
int &rAge =  a + b ; // 引用不能指向表达式
int const &rAge1 = a + b ;// 常引用可以指向表达式
```
4、 常引用可以指向不同的数据类型
```
int age = 20;
double &rAge = age; // 将4个字节的数据存在8个字节中,不允许
double const &rAge2 = age ; // 常引用可以存储不同的数据类型的值
```


5 const 参数的特点
![](/assets/Snip20190113_12.png)




