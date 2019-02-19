####  C++ 中的编码规范

**1、每个人都有自己的编程规范, 没有统一的标准, 没有标准答案, 没有最好的编码规范**

**2、C++ 中通用的变量名规范**

- **全局变量,g_ 开头, **
```
比如:定义全局变量: int g_age;
```

- **成员变量,m_ 开头**
```
比如:定义成员变量: int m_age;
```

- **静态变量,s_ 开头**
```
比如: 定义静态变量: static int s_age;
```

- **常亮,c_开头**
```
比如: 定义常亮: const int c_age;
```

- **静态全局变量,使用gs_ 开头**
```
比如: static int gs_count = 10;
```

- **静态成员变量, 使用ms_开头**
```
struct Person{
static int ms_Count;
};
int Person::ms_Count = 10;
```


- **静态成员常量, 使用msc_开头**
```
struct Person{
static const int msc_EyeCount;
};
const int Person::msc_EyeCount = 10;
```



使用驼峰表示,比如: int myAge; void doHomeWork();