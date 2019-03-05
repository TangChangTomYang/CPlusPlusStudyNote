#### lambda 表达式

**1、lambda 表达式有点类似于JavaScript中的闭包, iOS中的block, 其本事就是函数
**

**2、lambda 表达式完整的结构:
 `[`capture List`](`params List`)`mutable Exception -> return Type`{`
&emsp;&emsp;&emsp;function body
 `}`**
- **1> capture List: 是捕获外部变量的列表**
- **2> params List: Lambda表达式形参列表(不能所使用默认参数, 不能省略形参名)**
- **3> mutable: 用来说明是否可以修改捕获的外部变量(值捕获的外部变量)**
- **4> exception: 异常设定**
- **5> return type: lambda表达式(函数) 的返回值类型**
- **6> function body: lambda表达式的函数体**

**3、 有时,可以省略部分结构**
- **1> `[`capture List`](`params List`)`-> return type `{` function List `}`**
- **2> `[`capture List`](`params List`){`function body`}`**
- **3> `[`capture List`]{`function body`}`**