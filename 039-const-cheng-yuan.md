#### const 成员



<br>
#### 一、const 成员介绍
**1、const 成员: ** 被const 修饰的成员变量、非静态成员函数

<br>
**2、const 成员变量**
- 必须初始化(类内部初始化), 可以在声明的时候直接初始化赋值.
- 非 static 的 const 成员变量, 还可以在初始化列表中初始化.

<br>
**3、const 成员函数(非静态)**
- const 关键字写在参数列表的后面, 函数的声明和实现都必须带const
- 内部不能修改非static成员变量
- 内不只能调用const成员函数、static 成员函数
- 非const 成员函数可以调用const 成员函数
- const 成员函数和非const 成员函数构成重载
- 非const 对象(指针)优先调用非const成员函数
- const对象(指针)只能调用const成员函数、static 成员函数


<br>
**4、const函数 和 非const函数 构成函数重载**
- 当const函数和非const函数构成重载后, 非const对象 优先调用非const 函数. const 对象优先调用const函数


