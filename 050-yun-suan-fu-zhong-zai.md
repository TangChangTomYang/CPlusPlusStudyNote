#### 运算符重载


<br>
**1、运算符重载(operator overload)
,是C++的一个特性, 很多其它语言不支持运算符重载**



<br>
**2、C++ 里面不是所有的运算符都支持重载,有些运算符是不允许重载的,如下:**
- **对象成员访问运算符: '.'**
- **域运算符: '::'**
- **三目运算符: '?:'**
- **sizeof**



<br>
**3、有些运算符只能重载为成员函数,比如:**
- **赋值运算符: '='**
- **下标运算符: '[]'**
- **函数运算符: '()'**
- **指针访问运算符: '->'**





<br>
#### 运算符重载示例

```
class Point{
    friend Point operator+(const Point &p1, const Point &p2); // p + p
    friend ostream &operator<<(ostream &cout, const Point p); // cout << p;
    int m_x;
    int m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y){
    }
    
    
    /*Point p = p1 + P2; 重载 '+'

    这个'+'重载函数, 有多处语法技巧
    1>  参数使用const引用而不使用对象, 主要有2点
         1>> const引用可以接收 const 和 非const 参数. 
         2>> 函数参数使用引用不使用对象是避免产生中间临时对象
    2>  返回值使用匿名对象,避免使用对象作为函数返回值产生临时中间对象
    */
    Point operator+(const Point &p){ 
       return Point(this->m_x + p.m_x , this->m_y + p.m_y);
    }
    
    /* (p += P1) = p2; 重载 '+='

    这个'+='重载函数, 有多处语法技巧
    1> 引用作为函数的返回值, 返回值可以被再次赋值
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
    Point  operator++(int ){ // int 是语法糖固定写法
        Point p(this->m_x,this->m_y);
        this->m_x += 1;
        this->m_y += 1;
        return p;
    }
    
};

// Point p = p1 + p2; 我们要实现 '+' 号的运算符重载
Point operator+(const Point &p1, const Point &p2){ // 为了便于操作, 我们将这个方法定义为 Point 的友元函数
    
   return  Point(p1.m_x + p2.m_x, p1.m_y + p2.m_y); // 返回匿名对象, 避免中间对象的产生
}


/** 重载 << 打印point, cout << p;
 cout 是 ostream 类型的一个对象
 */
ostream &operator<<(ostream &cout, const Point p){ // 将这个重载运算符函数定义为Point的友元函数
   return  cout <<"(x = " << p.m_x << ",y = " << p.m_y << ")" << endl;
}

```