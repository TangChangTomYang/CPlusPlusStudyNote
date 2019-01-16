#### C++ 中的封装/继承/多台/Malloc/free/new/delete



<br>
#### 一、封装


**1、什么是封装? **
封装就是成员变量私有化, 提供公共的 getter 和 setter 给外界去访问成员变量.

```
struct Person {
private:
    int m_age;
    
public:
    void setAge(int age){
        m_ge = age;
        // 也可以这样写(等价的)
//        this -> m_age = age;
    }
    
    int age(){
        return m_age;
        // 也可以这样写(等价的)
//        return this -> m_age;
    }
}

int main(){
    Person pson;
    pson.setAge(10);
    cout << pson.age() << endl;
    
    getchar();
    return 0;
}
```









<br>
#### 二、程序的内存空间(每个程序在运行时都有一个独立的内存空间)

1、程序的内存空间的划分主要分成以下4个部分:

- **代码段(代码区)**<br>用于存放代码

- **数据段(全局区)**<br>用于存放全局变量等

- **栈空间**<br> 每调用一个函数就会给它分配一段连续的栈空间,等函数调用调用完毕后会自动回收这段栈空间 (栈平衡,调用时分配栈空间,调用完毕回收栈空间)

- **堆空间**<br> 需要主动去申请和释放


2、在程序的运行过程中, 为了能够自由的控制内存的生命周期/大小, 会经常用到堆空间.






<br> 
#### 三、堆空间的分配/ 回收
 


