#### 字符串常识


<br>
#### 
C语言中是允许 将一个字符串常量,比如: "bmw" 直接赋值给 char \* 的指针, 但是在C++ 是不允许的,在 C++ 中如果要将 一个字符串常量赋值给 char \* 指针 ,必须在char \* 指针前面加上 const 修饰符.如下:

```
// C语言中允许这样做
char *name = "bmw"; //  "bmw" 是一个常量字符串
printf("name: %s",name);

//C++ 的中,前面必须添加 const 修饰
const char *cppName = "bmw";
printf("cppName: %s",cppName);

```

