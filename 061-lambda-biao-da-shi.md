#### lambda 表达式



<br>
#### 一、lambda 表达式介绍
**1、lambda 表达式有点类似于JavaScript中的闭包, iOS中的block, 其本事就是函数
**

**2、lambda 表达式完整的结构:
 `[`capture List`](`params List`)`mutable Exception -> return Type`{`
&emsp;&emsp;&emsp;function body
 `}`**
- **1> capture List: 是捕获外部变量的列表**
- **2> params List: Lambda表达式形参列表(不能所使用默认参数, 不能省略形参名)**
- **3> mutable: 用来说明是否可以修改捕获的外部变量(值捕获的外部变量)**
- **4> exception: 异常设定**
- **5> return type: lambda表达式(函数) 的返回值类型**
- **6> function body: lambda表达式的函数体**

**3、 有时,可以省略部分结构**
- **1> `[`capture List`](`params List`)`-> return type `{` function List `}`**
- **2> `[`capture List`](`params List`){`function body`}`**
- **3> `[`capture List`]{`function body`}`**






####二 、lambda表达式示例

**1、有参数有返回值类型lambda 表达式**

**因为Lambda 表达式的本质是一个函数, 因此我们可以使用一个指向函数的指针,接收它
lambda表达式中的捕获列表必须有, 但是可以没有捕获内容(内容为空)**
```
void demo1(){
    
    // 可以使用 指向函数的指针接收
    int (*p)(int a, int b) = [](int a, int b) -> int{
        cout << "a: " << a << ",b: " << b << endl;
        return a + b;
    };
    
    p(10, 20);
    
    
    // 如果不知道返回值的类型也可以使用auto 类型的变量, 系统自动推导
    auto a1 =  [](int a, int b) -> int{
        cout << "a: " << a << ",b: " << b << endl;
        return a + b;
    };
    a1(1,3);
}
```


<br>
**2、 有参数 无返回值类型**

**lambda 表达式类型可以省略, 系统会推到出返回值类型**
```
void demo2(){
    // 系统会推到出 lambda 表达式的返回值类型为 int
    int (*p1)(int a, int b) = [](int a, int b){
        cout << "a: " << a << ",b: " << b << endl;
        return a + b;
    };
    p1(11, 22);
}
```



<br>
**3、 无参数 有返回值类型**
```
void demo3(){
    
    int (*p1)() = []()->int{
        cout << 110 << endl;
        return 110;
    };

    auto p2 = []()->int{
       cout << 10 << endl;
        return 10;
    };

    p1();
    p2();
    
}
```
