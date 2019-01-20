#### C++ 继承

1:20继承
1:40



#### 一、成员访问权限

**1、成员访问权限、继承的方式有3种.**
1>**public:** 公共的, 任何地方都可以访问(struct 默认)

2>**protected:** 子类内部、当前类内部可以访问

3>**private:** 私有的, 档案类内部可以访问(class 默认)



<br>
#### 二、访问权限 使用情景1(修饰内部成员(成员变量和方法))
 
```
struct Person{
    public:
    int m_age;
    protected:
    double m_height;
    privated:
    int m_money;
}
```


<br>
#### 三访问全现房 使用情景2(选择继承的方式)
```

struct Person{
    public:
    int m_age;
    protected:
    double m_height;
    privated:
    int m_money;
}


struct Student : Person{ // 默认就是public 继承
    int m_score;
}

struct GoodStudent : protected Student{ // 修饰继承方式

    void work(){
        cout << "void work()" << endl;
    }
}
```

#### 三 子类内部访问父类成员的权限, 是以下2项权限中最下的那个

- 成员本身的访问权限
- 上一级父类的集成方式

在开发中用的最多的继承2方式是 public(默认就是), 这样能保留父类原来的成员访问权限















