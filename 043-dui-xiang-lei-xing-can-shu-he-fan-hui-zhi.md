
#### 对象类型参数和函数返回值


 
**1、C++中, 将对象 作为函数的参数 或者 函数的返回值, 可能会产生一些不必要的中间对象** C++ 中有这种现象, 其它像java/OC 不用关心

**分析**
- **1> 在C++ 中,将对象数据类型作为函数的参数使用时, 为什么会产生中间对象呢?**
    - **其实, 这是C++出于数据安全的一种处理对策. 事想一下, C++中的对象可以是栈空间的(自动回收)/ 也可以是堆空间的(程序员控制声明周期), 你将一个对象传给一个函数, 函数怎么知道这个对象是哪一种(栈对象 还是 堆对象),他的生命周期如何, 为了数据安全, 编译器只好调用拷贝构造生成一个新的对象, 这也就是为什么在C++中将对象作为函数的参数, 系统会调用拷贝构造产生一个 临时对象的原因**
    
    - **对象类型数据作为函数参数可能产生临时对象示例:**


        ```
        class Car{
            int m_price;
        public:
            // 构造函数
            Car(int price = 0) : m_price(price){
                cout << "构造 Car , price:" << m_price << "---address: " << this << endl;
            }
            
            // 拷贝构造
            Car (const Car &car) : m_price(car.m_price){
                cout << "拷贝构造 Car , price:" << m_price << "---address: " << this << endl;
            }
            
            // 析构函数
            ~Car(){
                cout << "析构 ~Car Address: " << this << endl;
            }
            
        };
        
        // 相当于 void test(Car car = car), 这里就是拷贝.
        // 或者 相当于 void test(Car car = Car(car))
        void test(Car car){
            cout << "测试 car" << endl;
        }
        
        // 中间对象解决方案, 不要直接使用对象作为函数参数, 而是使用对象的指针或者是对象的引用
        void test_p(Car *car){
            cout << "测试 *car" << endl;
        }
        void test_yy(Car &car){
            cout << "测试 &car" << endl;
        }
        
        
        int main() {
            {
                Car myCar(10);
                test(myCar); // 会产生中间对象
            }
            cout << "----以下是解决方案-------" << endl;
            {
                Car myCar2(20);
                test_p(&myCar2); //对象指针 不会产生中间对象
                test_yy(myCar2); //对象引用 不会产生中间对象
            }
            getchar();
            return 0;
        }
        
        // 打印 结果
        构造 Car , price:10---address: 0x7ffeefbff4f8
        拷贝构造 Car , price:10---address: 0x7ffeefbff4f0
        测试 car
        析构 ~Car Address: 0x7ffeefbff4f0
        析构 ~Car Address: 0x7ffeefbff4f8
        ----以下是解决方案-------
        构造 Car , price:20---address: 0x7ffeefbff4e0
        测试 *car
        测试 &car
        析构 ~Car Address: 0x7ffeefbff4e0
        ```
        

**3 对象作为函数的返回值, 产生中间对象**

```
// 对象作为函数的返回值, 产生中间对象的示例
Car testCar(){
    Car car(20);
    return car;
}
```