
#### C++ 中的封装


<br>
#### 一、封装


**1、什么是封装? **
- **封装就是成员变量私有化, 提供公共的 getter 和 setter 给外界去访问成员变量.**

- **其实封装有很多好处, 有了封装之后,外面的人员在使用时更安全 更便捷 .(比如细节的屏蔽/ 数据的拦截/ 特别是涉及数据拷贝时能有效解决数据的安全问题等等)**

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









