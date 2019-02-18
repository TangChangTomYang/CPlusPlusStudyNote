#### 运算符重载


**1、运算符重载, 是C++的一个特性, 很多其它语言不支持运算符重载**
**2、C++ 里面不是所有的运算符都支持重载**




<br>
#### 运算符重载示例

```
class Point{
    int m_x;
    int m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y){
    }
    
    
    /*Point p = p1 + P2; 重载 '+'

    这个'+'重载函数, 有多处语法技巧
    1>  参数使用const引用而不使用对象, 主要有2点(1. const引用可以接收 const 和 非const 参数. 2. 函数参数使用引用不使用对象是避免产生中间临时对象)
    2>  返回值使用匿名对象,避免使用对象作为函数返回值产生临时中间对象
    */
    Point operator+(const Point &p){ 
       return Point(this->m_x + p.m_x , this->m_y + p.m_y);
    }
    
    /* (p += P1) = p2; 重载 '+='

    这个'+='重载函数, 有多处语法技巧
    1>  引用作为函数的返回值, 可以被赋值
    2> 引用作为函数返回值,避免对象作为函数返回值产生临时对象
    */

    Point &operator+=(const Point &p){
        this->m_x += p.m_x ;
        this->m_y += p.m_y ;
        
        return *this;
    }
    
     // 重载 '++p' 号 运算符
    Point &operator++(){
        this->m_x += 1;
        this->m_y += 1;
        return *this; // 返回的是引用, 避免产生临时中间对象
    } 
    
    // 重载 'p++' 号 运算符
    void  operator++(int ){ // int 是语法糖固定写法
        this->m_x += 1;
        this->m_y += 1;
        
    }
    
};
```