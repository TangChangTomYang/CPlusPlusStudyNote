#### 一、汇编语言了解(程序/电脑中内存的划分)

![](/assets/Snip20190116_3.png)


**每个应用都有自己独立的内存空间, 其内存空间一般都有以下几大区域:**
- **代码段(代码区)**<br>用于存放代码

- **数据段(全局区)**<br>用于存放全局变量等

- **栈空间**<br> 每一次调用函数就会给当前函数分配**(push)**一段连续的栈空间,等函数调用完毕后会自动回收**(pop)**这段栈空间 
**(函数内定义的临时变量一般分配的都是栈空间, 栈空间不用程序员管理内存)**
**(栈平衡,调用时分配栈空间,调用完毕回收栈空间)**

- **堆空间**<br> 需要主动去申请和释放 
```
   Person *pson = new Person(); // 在堆空间分配一个存储空间用来存储Person对象
   delete pson; // 堆空间内存管理, 一个new 对应一个delete

   int *p = new int(10); 在 堆空间分配4个字节(或者8个字节)用于存储10;
   delete p;
```


<br>
####二、汇编语言的种类:
- 8086汇编(16位)
- x86汇编(32位)
- x64汇编(64位)
   -  x64汇编根据编译器的不同, 有2种书写格式
      - intel 汇编
      - AT&T 汇编
- arm汇编 (嵌入式/ 移动设备)

<br>
**注意点:**
**汇编语言(汇编指令)是不区分大小写的**







<br>
#### 二、AT&T汇编 VS Intel 汇编

|项目|AT&T|Intel| 说明|
|-|-|-|-|
|寄存器名称| %eax|eax|Intel的不带% <br> AT&T 汇编需要在 寄存器名字前加 % 号|
|操作数顺序| movl %eax, %edx| mov edx, eax| 将eax 的值赋值给edx <br> intel 的是从右往左赋值, AT&T 是从左往右|
|常数\立即数|movl $3, %eax <br> movl $0x10 ,%eax| mov eax,3 <br> mov eax,0x10| 将3赋值给eax <br> AT&T 的立即数需要在前面加 $ 符号|
|jmp 指令| jmp `*`%edx <br> jmp `*`0x4001002<br> jmp `*`(%eax)| jmp edx <br> jmp 0x4001002 <br> jmp [eax] `(跳转到内存地址)`| AT&T汇编中 jmp 指令地址前面要使用 `*` 修饰说明, |
|操作数长度| movl %eax,%edx <br> movb $0x10, %al <br> leaw 0x10(%dx),%ax| mov edx, eax<br> mov al, 0x10<br> lea ax,[dx+0x10]|`b`=byte(8bit)<br> `s`=short(16bit  或 32bit ) <br> `l`=long(32bit 或 64bit) <br> `q`=quad(64bit) <br> `t`=ten bytes(80 bit)|



**一般规律:**
**R 开头的寄存器是64bit 的, 占8个字节
E 开头的寄存器是32bit 的, 占4字节**



<br>
#### 三、x64汇编要点总结

- **mov dest, src **
将src 的内容赋值给 dest, 类似于 dest = src

- **[地址值]**
中括号[ ]里面放的都是内存地址

- **word 是2字节, dword 是4字节(double word), qword 是 8 个字节(quad word)**

- **call 函数地址**
调用函数

- **lea dest, [地址值]**
将地址值赋值给dest, 类似于 dest = 地址值,比如:
```
int *p = NULL;
int a = 10;
p = &a; // 此处即要用到 lea eax, [xxx];
```

- ret 
函数返回

- xor op1, op2
将 op1 和 op2 异或的结果赋值给op1, 类似于 op1 = op1 ^ op2;

- add op1, op2
类似于 op1 = op1 + op2;

- sub op1, op2
类似于 op1 = op1 -op2;

- inc op  //increase
自增, 类似于 op = op + 1;

- dec op  //decrease
自减, 类似于 op = op -1;

- jmp 内存地址   // 类似于go to 语句  
跳转到某个内存地址去执行代码
j 开头的一般都是跳转, 大多数是带条件的跳转, 一般跟 test/ cmp 等指令配合使用.








<br>
#### 四、汇编语言范例

```
int a = 1;
mov dword ptr [ebp - 8],1 

int b = 2;
mov dword ptr [ebp - 14h], 2

int c = a + b;
mov eax, dword ptr [ebp - 8] // 一个变量的地址值,是他最小的地址值, 内存从低到高存储
add eax, dword ptr [ebp - 14h]
mov dword ptr [ebp - 20h], eax
```


给函数分配的内存空间: **栈空间 ** (入栈 push/ 出栈pop)
栈空间的特点:

```
int a = 5;
mov dword ptr [ebp -0ch], 5 // 将5存入[ebp -0ch]内存
int *p = &a;
lea eax, [ebp - och]  // 将内存地址 [ebp - och
] 存入寄存器
mov dword ptr [ebp - 18h], eax // 将寄存器值存入内存地址
*p = 6;
mov eax, dword ptr [ebp -18h] // 将内存中的数据存入寄存器
mov dword ptr [eax], 6 // 将值存入寄存器对应的内存

```




























