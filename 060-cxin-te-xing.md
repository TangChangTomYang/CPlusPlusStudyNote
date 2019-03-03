#### C++ 新特性


#### auto
**1 可以从初始化表达式中推断出变量的类型, 大大简化编程工作**
**2 属于编译器特性, 不影响最终的机器码质量, 不影响运行效率**
```
// 以前我们定义变量, 是这样的 (指定变量的类型)
int a = 10;
double d = 20.0
Person *p = new Person(10);
p->m_age = 30;

// 新编译器使用auto, 编译器自动推到出类型
auto a = 10;
auto d = 20.0
auto *p = new Person(10);
p->m_age = 30;
```




#### decltype
**1 可以获取变量的类型**
```
int a = 10;
decltype(a) b = 20; // int 
有点
typeof(self) weakSelf = self; 的感觉
```


#### nullptr
**1 可以解决NULL的二义性问题**
**2 专门用于清空指针的**

```
void func(int a){
    cout << "void func(int a) " << a << endl;
}

void func(int *a){
    cout << "void func(int *a) " << a << endl;
}

func(0);
func(NULL); // 以前使用 NULL 相当于0,会有二义性
func(nullptr); // nullptr 就是空指针

int a = 0;
int *p = &a;
p = NULL ;
p = nullptr; // 现在清空指针一般使用nullptr
```



#### 遍历
```
// 以前是这样的
int array[] = {10,20,30,40};
int length = sizeof(array)/ sizeof(int);
for (int i = 0 ; i < length ; i++){
    cout << array[i] << endl;
}

// 现在可以这样
for (int item in array){
    cout << item << endl;
}
```


#### 更简单的初始化方式
```
// 以前
int array[] = {10,20,30,40};

// 现在, 直接省略 = 
int array{10,20,30,40};
```







#### Lambda 表达式
**1 Lambda 表达式, 有点类似于javaScript中的闭包/ iOS 中的Block/ 本质就是函数**
```
int p(int a, int b) = [](int a, int b)-> int{
    return a + b;
};

p (10, 20);
```
1:25