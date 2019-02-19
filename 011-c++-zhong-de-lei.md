#### C++ 中的类


**1、C++ 中可以使用 struct/ class 来定义一个类.**
在C++中使用 Struct 和 class 来定义的类本质上是没有什么区别的, 只是在编译器层面, struct 定义的类 默认继承方式和访问权限都是 Public, 而使用class 定义的类默认继承方式和访问权限是private.即如下图: 

![](/assets/Snip20190219_7.png)


<br>
**2、struct 和 class的相同点和不同点? **

1> 在C++ 中 struct 和 class 都可以用来定义一个类.
2> 当使用struct定义类是,默认的成员权限是 public. 而 使用 class 来定义类时,默认的成员权限是 private.

![](/assets/Snip20190115_5.png)









<br>
**3、 在栈空间的C++ 对象**
![](/assets/Snip20190115_6.png)
在Objective 或者 就java 中, 对象只能在对空间,但是在C++中对象可以在栈空间也可以在对空间.





<br>
**4 通过指针访问对象的成员变量和成员方法, 和访问结构体是一样的**
![](/assets/Snip20190115_7.png)
如果是对象访问成员变量或者成员方法,直接用点语法.
如果是通过指正访问成员变量或者成员方法, 则用 -> 来访问

