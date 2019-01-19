#### C++ 中 类 声明 和 实现分离

类 声明 和 实现分离, 就是说类的声明单独写, 类的实现单独写.



<br>
#### 类 声明和实现分离,方式一:
声明实现写在同一文件内, 使用 域 (比如: Student::) 做限定
```
/*********以下是类的声明部分*****************************************/
class Student{ // 声明一个类

    int m_age;
    double m_height;
    
public: // 以下都是类的对外接口
    // 声明构造函数和析构函数
    Student();
    ~Student();
    
    // 声明 对外的属性接口
    int age();
    void setAge(int age);
    double height();
    void setHeight(double height);
};


/*********以下是类的实现部分*****************************************/
// 类分离和实现分开时, 域(::)直接写在析构函数和构造函数的前面做限定即可
Student::Student(){
    cout << "Student :: Student()" << endl;
}

Student::~Student(){
    cout << "Student :: ~Student()" << endl;
}


// 类分离和实现分开是, 域(::) 需要写在函数返回值的类型后面,在类提供的接口函数名前面做限定
int  Student::age(){
    return this -> m_age;
}

void Student::setAge(int age){
    this -> m_age = age;
}

double Student::height(){
    return this -> m_height;
}

void Student::setHeight(double height){
    this -> m_height = height;
}


// 外面访问
int main(){
    Student *stu = new Student();
    stu -> setAge(18);
    stu -> setHeight(2.2);
    
    cout << "age =" << stu -> age() << "height =" << stu -> height() << endl;
    
    delete stu;

    return 0;
}
```










<br> 
#### 方式二: .hpp 文件声明, .cpp 文件实现
