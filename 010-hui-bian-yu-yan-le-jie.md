#### 汇编语言了解

<br>
####一、汇编语言的种类:
- 8086汇编(16位)
- x86汇编(32位)
- x64汇编(64位)
   -  x64汇编根据编译器的不同, 有2种书写格式
      - intel 汇编
      - AT&T 汇编
- arm汇编 (嵌入式/ 移动设备)


汇编语言时不区分大小写的


<br>
#### 二、AT&T汇编 VS Intel 汇编

|项目|AT&T|Intel| 说明|
|-|-|-|-|
|寄存器名称| %eax|eax|Intel的不带%|
|操作数顺序| movl %eax, %edx| mov edx, eax| 将eax 的值赋值给edx|
|常数\立即数|movl $3, %eax <br> movl $0x10 ,%eax| mov eax,3 <br> mov eax,0x10| 将3赋值给eax|
|jmp 指令| jmp *%edx <br> jmp *0x4001002<br> jmp *(%eax)| jmp edx <br> jmp 0x4001002 <br> jmp [eax]| 在AT&T的jmp地址前面要加 型号 *|
|操作数长度| movl %eax,%edx <br> movb $0x10, %al <br> leaw 0x10(%dx),%ax| mov edx, eax<br> mov al, 0x10<br> lea ax,[dx+0x10]|



一般规律:
R 开头的寄存器是64bit 的, 占8个字节
E 开头的寄存器是32bit 的, 占4字节































