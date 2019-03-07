#### 字符串常识


<br>
#### 一、 C++ 与 C 语言中 字符串指针的差异

**1、C语言中是允许 将一个字符串常量`(比如: "bmw")` 直接赋值给 char \* 的指针, 但是在C++ 是不允许的**

**2、在 C++ 中如果要将 一个字符串常量`(比如: "bmw")`赋值给 char \* 指针 ,必须在char \* 指针前面加上 const 修饰符.如下:**

```
// C语言中允许这样做
char *name = "bmw"; //  "bmw" 是一个常量字符串
printf("name: %s",name);

//C++ 的中,前面必须添加 const 修饰
const char *cppName = "bmw";
printf("cppName: %s",cppName);

```


<br>
#### 二、C++ 中 和 C语言中接收字符串指针的函数参数的设置

**C++ 中 const 参数,可以接收const 和 非 const 实参**
```
char *name = "zhangsan";
char address[] = {'C','D','\0'};

// C 语言中可以 这样来定义一个函数来接收外面的字符串
void display(char *name){
    printf("name: %s",name);
}

display(name);
display(address);


// C++ 中必须这样定义, 才能接收非const 字符串和const 字符串
void cpp_display(const char *name){
    cout << "name:" << name <<  endl;
}
cpp_display(name);
cpp_display(address);

```






