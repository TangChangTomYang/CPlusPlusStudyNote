####  #pragma once 与 条件编译


<br>
#### 一、 条件编译

1、在C语言的使用中, 我们经常用 **#ifndef/ #define/ #endif (条件编译)**来防止头文件的内容被重复包含,如下图:

![](/assets/Snip20190112_5.png)


<br>
#### 二、 #pragma once
2、**#pragma once** 同样可以防止整个文件的内容被重复包含, 只是高版本的C++ 编译器才支持

![](/assets/Snip20190112_8.png)
的




####三、  #pragma once 与 条件编译 的优缺点

1、**#pragma once** 只能在较高版本的C++ 环境中才能使用, 使用简单一行代码


2、 基本所有的编译器都支持 **条件编译** , 缺点要写多行代码
