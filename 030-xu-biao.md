#### 虚表


**虚函数的实现原理是虚表, 这个虚表里面存储着最终需要调用的虚函数地址, 这个虚表也叫虚函数表**

```
class Anima{
public:
    int m_age;
    virtual void speak(){
        cout << "Anima::speak()" << endl;
    }
};

class Cat : public Anima{
public:
    int m_life ;
    void speak(){
        cout << "Cat::speak()" << endl;
    }
    void run(){
        cout << "Cat::run()" << endl;

    }
};

Animal *cat = new Cat();
cat->m_age = 20;
cat->speak();
cat->run();
```
![](/assets/Snip20190304_2.png)
**所有的Cat 对象, 不论是在全局区/ 栈区/ 堆区 公用同一份虚表**