#### C++ 11 新特性

**auto/ decltype/ nullptr/ 数组快速遍历/ 数组快速初始化**



<br>
#### 一、auto 关键字定义变量类型

**1、C++ 11 中新增了 使用 auto 关键字用来定义变量的特性**
**2、使用auto关键字定义变量时, 我们不在关心变量的具体类型, 编译器会在初始化表达式中根据 右侧的表达式,自动推到出变量的具体类型**
**3、auto 推到, 支持所有的数据类型, 特别是在有些时候不好定义变量类型时, 使用auto 定义变量很方便**
**4、auto 数据类型推导, 是属于编译器层面的特性, 不会影响最终的机器码质量, 不影响运行效率**

<br>**示例如下: **
```
void autoDemo(){
    auto i = 10; // int
    auto str = "C++"; // const char *
    auto p = new Person(); // Person *
    p->run();
}
```





<br>
#### 二、decltype 获取变量的数据类型

**1、 decltype 的英文意思是解密的意思, C++ 11 中新增decltype 关键字, 用于获取变量的数据类型**

<br>**示例如下: **
```
// 当我们要定义一个和已知变量相同类型的数据时, 使用decltype 很方便
void decltypeDemo(){
    int a = 10;
    
    decltype(a) b = 20;
    cout << "a: " << a << ",b: " << b << endl;
    
    // 自动获取变量的类型为 Person *
    auto p = new Person();
    decltype(p) pson = new Person();
    pson->run();
}
```