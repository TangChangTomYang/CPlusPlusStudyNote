#### 友元

** 友元包含友元函数和友元类**

 **1、如果将函数A (非成员函数) 声明为 类C 的友元函数, 那么函数A 就能直接访问 类C 对象的所有成员**
 **2、 如果将类A声明为类C的友元类, 那么类A的所有成员函数都能直接访问类C对象的所有成员**
 **3、 友元类破坏了面向对象的封装性, 但是在某些频繁访问成员变量的地方可以提高性能**
 
 ```
 class Point {
    // 将外部的函数(void friendDisplay(Point point)) 声明为友元函数
    friend  void friendDisplay(Point point);
    // 将一个类声明为友元类
    friend class Math;
private:
    int m_x;
    int m_y;
public:
    int getX(){ return m_x;}
    int getY(){ return m_y;}
    Point(int x, int y) : m_x(x), m_y(y){
        
    }
};

//非友元函数内部 不可以, 通过对象直接访问 对象内的私有成员变量
void display(Point point){
    // 不允许访问
//    cout << "x: " << point.m_x << ", y: " << point.m_y << endl;
    
    // 只能这样访问
    cout << "x: " << point.getX() << ", y: " << point.getY() << endl;
    
}

//友元函数内部可以通过 对象直接访问 对象内的私有成员变量(就像在类自己里面操作一样)
void friendDisplay(Point point){
    cout << "x: " << point.m_x << ", y: " << point.m_y << endl;
}


// 友元类内部, 可以通过对象直接访问其内部的私有成员变量(就像在类里访问一样)
class Math{
    
    void testPoint (Point &point){
        
        if(point.m_x < 10){
            point.m_x = 10;
        }
        if(point.m_y < 20){
            point.m_y = 20;
        }
    }
    
    static void test22Point (Point &point){
        
        if(point.m_x < 10){
            point.m_x = 10;
        }
        if(point.m_y < 20){
            point.m_y = 20;
        }
    }
}

```