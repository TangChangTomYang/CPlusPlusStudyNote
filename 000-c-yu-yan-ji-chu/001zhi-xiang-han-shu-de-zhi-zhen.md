#### 一、指针
![](/assets/Snip20190112_1.png)

#### 二、指向函数的指针
1、指向函数的指针
![](/assets/Snip20190111_1.png)

在使用指向函数的指针时, 系统也会提示:
![](/assets/Snip20190111_3.png)


<br>
#### 三、指向函数的指针, 作为函数的参数

![](/assets/Snip20190111_4.png)


<br>
#### 四、结构体/ 指向结构体的指针
```
结构体成员变量访问的方式
Student {
    int age;
    int weight;
};

// 结构 体访问成员变量
Student stu = {10, 20};
stu.age = 20;
stu.weight = 40;

// 结构体指针
Student *stu1 = &stu;
stu1 -> age = 30;
stu1 -> weight = 40;
```






