#### 函数重载\ 内联函数\ extern

1、在java 的世界里, 先有类, 再有方法(函数), 如下图:
![](/assets/helloJava.png)
C++ 中方法(函数),必须写在类里面.


<br>
2、在C++ 不需要类, mian 函数即是程序的入口. C++ 不像java(可以有多个main函数) 只能有一个main函数

![](/assets/Snip20190109_5.png)


3、C++ 中的输出

```
void testOutput(){
    cout << "C++ 中输出内容使用 cout ,  << 和输出内容成对出现即可" << endl;
}
```

4、C++ 中的输入
```
void testInput{
    int a;
    // 在C++中输入, 不需要在变量前面加 & 符号
    cin >> a ;
    cout << "a = " << a << endl;
}
```


