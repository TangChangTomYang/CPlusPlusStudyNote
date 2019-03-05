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




<br>
#### 三、nullptr 空指针关键字
**1、 在C++ 11 中新增了 nullptr 空指针关键字, 专门用于清空指针**
**2、 因为 NULL 和数字0 是等价的, 因此一个为NULL的指针变量和为 0 的int 变量很难分开, 会产生二义性, 因此在 C++11 中出现了 nullptr **
**3、 nullptr 就是专门用于解决 int=0的变量和 int`*`=0 的指针的二义性的**


<br>**示例如下: **
```
void func(int  a){
    cout << "void func(int " << a << ")"<< endl;
}

void func(int  *p){
    cout << "void func(int *" << p << ")"<< endl;
}
// nullptr 专门用于清空指针 (替代NULL)
// 解决 NULL带来的二义性(NULL == 0)问题
void nullptrDemo(){
    
    func(0);
    func(nullptr); // 等价于 int *p = null, 是一个空指针
    //func(NULL);  // 系统不知道是调用哪一个, 有二义性
    
    if (NULL == 0) {
        cout << "NULL == 0, 即NULL完全等价于0" << endl;
    }
}
```







<br>
#### 四、数组快速遍历 (for(xxx : yyy)) 与 更简洁初始化新特性

<br>**示例如下: **
```
// 快速遍历新特性
void kuaiSuBianliDemo(){
    int arr[] = {1,2,3,4,5,6,7};
    for (int  item : arr){ // 快速遍历使用的是 : 冒号, 而不是 in 关键字
        cout << "item: "  << item << endl;
    }
    
    // 更加简洁的初始化
    int arr2[]{11,12,3,14,15,16,17}; // 快速初始化, 可以省略 赋值运算符 '='
    for (int item : arr2){
       cout << "---item: "  << item << endl;
    }
}
```