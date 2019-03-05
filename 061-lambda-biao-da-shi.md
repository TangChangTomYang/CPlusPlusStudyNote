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





<br>
**4、 无参数 无返回值类型**

```
void demo4(){
    auto p1 = []{
        cout << "无参数, 无返回值类型 lambda1"<< endl;
    };
    p1();
    
    auto p2 = [](){
        cout << "无参数, 无返回值类型 lambda2"<< endl;
    };
    p2(); 
}
```



<br>
***5、 可以使用 auto 类型的变量来接收 lambda 表达式**
```
void demo5(){
    auto p1 = [](int a, int b)->int{
        cout <<"(a " << a << ", b " << b << ")" << endl;
        return a + b;
    };
    p1(9,20);
    
    auto p2 = [](int a, int b){
        cout <<"(a " << a << ", b " << b << ")" << endl;
        return a + b;
    };
    p2(19,120);
}
```



<br>
#### 三、lambda 表达式 --> 外部变量的捕获

**1、外部变量 值捕获**
```
void captureDemo1(){
    int a = 10;
    int b  = 20;
    
    
    auto func =  [a,b]{//值捕获, 被捕获的变量值在lambda 表达式被赋值时就确定了
        cout << "值捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
10
20
```





<br>
**2、隐式 值捕获**
```
void captureDemo2(){
    int a = 110;
    int b  = 210;
    
    
    auto func = [=]{//值捕获, 被捕获的变量值在lambda 表达式被赋值时就确定了
        cout << " 隐式 值捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
10
20
```





<br>
**3、a 值捕获, 其它地址捕获**
```
void captureDemo3(){
    int a = 110;
    int b  = 210;
    int c  = 310;
    //值捕获, 被捕获的变量值在lambda 表达式被赋值时就确定了
    //地址捕获, 被捕获的变量的值在 lambda 表达式在被调用时刻才能确定
    auto func =  [&, a]{
        cout << " a 值捕获, 其它地址捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
        cout << c << endl;
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
10
22
310
```



<br>
**4、a 地址捕获, b值捕获**
```
void captureDemo4(){
    int a = 110;
    int b  = 210;
    int c  = 310;
    //值捕获, 被捕获的变量值在lambda 表达式被赋值时就确定了
    //地址捕获, 被捕获的变量的值在 lambda 表达式在被调用时刻才能确定
    auto func =  [&a, b]{
        cout << "a 地址捕获, b值捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
//        cout << c << endl; 变量c未被捕获, 不能使用
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
11
210
```


<br>
**5、隐式 地址捕获**
```
void captureDemo5(){
    int a = 110;
    int b = 210;
    int c = 330;
    auto func =  [&]{
        cout << "隐式地址捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
        cout << c << endl;
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
11
22
330
```




<br>
**6、a地址捕获, 其它隐式值捕获**
```
void captureDemo6(){
    int a = 110;
    int b = 210;
    int c = 330;
    auto func =  [=, &a]{
        cout << "隐式地址捕获"<< endl;
        cout << a << endl;
        cout << b << endl;
        cout << c << endl;
    };
    a = 11;
    b = 22;
    func();
    a = 111;
    b = 222;
}
// 打印结果:
11
210
330
```




<br>
#### 四、lambda 表达式 mutable 修改外部捕获的变量
```
// lambda 表达式 mutable 修改外部捕获的变量
void mutalbeDemo1(){
    int a = 0;
    int b = 1;
    cout <<"lambda 表达式 mutable 修改外部捕获的变量" << endl;
//    auto  func = [=]()mutable{
    auto  func = [&]()mutable{ // 捕获表达式必须为 地址捕获才 且 mutable 关键字(有无都可以) 可以修改 外部捕获变量的值
//    auto  func = [a,b](){ // 捕获表达式必须为 地址捕获才可以修改 外部捕获变量的值
        a = 110;
        b = 220;
        cout <<"lambda 表达式 mutable change" << endl;
    };
    cout << "a= " << a << endl;
    cout << "b= " << b << endl;
    func();
    cout << "a= " << a << endl;
    cout << "b= " << b << endl;
}

```
