---
title: GDB基础
toc: true
date: 2018-08-23 16:37:41
tags: [debugging, gdb]
categories: [debugging]
---

# GDB 调试

------

我们在进行代码创作的时候, 不可避免会产生bug, 即使没有bug. 我们想要知道程序运行过程中的输出或者程序运行的情况, 以便于我们更好的管理程序或者随心所欲的操纵程序, 虽然大多数IDE已经集成的debug的功能, 但是在Bash中我们用vim进行创作, GDB的调试就必不可少, 可以发挥储更强大的功能, GDB虽小, 但是他的功能却是很强大的, 正所谓 "麻雀虽小, 五脏区全".

------
## 何为GDB
**wikipedia** 如是说:
[The GNU Debugger (GDB)](https://en.wikipedia.org/wiki/GNU_Debugger)  is a portable debugger that runs on many Unix-like systems and works for many programming languages, including Ada, C, C++, Objective-C, Free Pascal, Fortran, Go, Java[1] and partially others.         
GDB就是运行在 **Unix-like** 平台上的GUN软件系统的调试器, 也就是说是一个专门进行调试的软件.
到目前为止, GDB已经支持以下的语言:
> * Ada
> * Assembly
> * C
> * C++
> * D
> * Fortran
> * Go
> * Objective-C
> * OpenCL
> * Modula-2
> * Pascal
> * Rust

[GDB官网](http://www.gnu.org/software/gdb/) 在官网中我们可以下载到最新版本的GDB, 并且了解到的最新信息

[GDB-toturial](https://sourceware.org/gdb/onlinedocs/gdb/) GDB调试参考

一般情况下, GDB可以帮助我们进行一下功能:
*参考至文献[ [2.](https://blog.csdn.net/haoel/article/details/2879)]*
> * 启动你的程序，可以按照你的自定义的要求随心所欲的运行程序。
> * 可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
> * 当程序被停住时，可以检查此时你的程序中所发生的事。
> * 动态的改变你程序的执行环境。
------
## GDB调试
在这里我只演示我们平时用的比较多的语言:
> - [ ] Ada
> - [ ] Assembly
> - [X] C
> - [X] C++
> - [ ] D
> - [ ] Fortran
> - [ ] Go
> - [ ] Objective-C
> - [ ] OpenCL
> - [ ] Modula-2
> - [ ] Pascal
> - [ ] Rust

------

<h4> 1. **GDB 命令介绍** </h4>

调试命令: ***For C/C++***

> 1. 在编译时将调试信息加入到可执行文件中
```
// -g 参数将调试信息加入到可执行文件中  -Wall 参数在编译后显示所有警告
gcc -g -Wall helloworld.c
g++ -g -Wall helloworld.cpp
//编译完成后生成 a.exe 文件
```
<img src="/assert/debug/gdb/1.jpg" width="1230">
<br>
> 2. 通过GDB执行a.exe 文件, 两种执行方式.
```
gdb [filename]
gdb
file [filename]
```
<img src="/assert/debug/gdb/2.jpg" width="1230">
<br>
> 3. 进行调试
调试一般分为以下几个步骤:
    1. 添加断点
    2. 查看断点信息
    3. 执行调试
    4. 查看调试输出信息

-------

<br>
在调试之前, 我先介绍以下GDB调试时候常用的几个命令:
<br>

>| 功能     |   命令   |
| ------ | ------|
|文件清单| list / l |
|执行程序| run / r |
|显示数据| print / p, whatis|
|断点设置| break / b, info break, clean delete|
|单步进入| next / n, step, finish, until |
|文件搜索| serach |



<br>
<h4> list </h4>

*参考至文献[ [7.](https://blog.csdn.net/sfeng177/article/details/53014289)]*

> list 命令用于列出代码, l 与其作用相同
```
//list 命令的作用是在控制台上显示代码信息
list (l) 从中间显示前后10行
list + 向后显示10行
list - 向前显示10行
list [line number] 显示line number前后10行
list [function] 显示名为function的函数前后10行
list listsize <count> 设置一次性显示代码行数
show listsize 显示一次性显示行数
list <start>, <end> 显示从start到end行的代码
list , <end> 显示从当前行到end行的代码
```
<img src="/assert/debug/gdb/3.jpg" width="1230">
<br>
<h4> break </h4>

*参考至文献[ [8.](https://blog.csdn.net/yangzhongxuan/article/details/6897968)]*
> 相关命令有break，tbreak，rbreak,hbreak，thbreak，后两种是基于硬件的，先不介绍。
>break，tbreak可以根据行号、函数、条件生成断点。tbreak设置方法与break相同，只不过tbreak只在断点停一次，过后会自动将断点删除，break需要手动控制断点的删除和使能。
```
//break的参数
break linenum 指定行号添加断点
break filename:linenum 指定文件行号条件断点
break function 指定函数添加断点
break filename:function 指定文件函数添加断点
break condition 指定条件添加断点
break *address 指定地址添加断点(可以通过 info add + (变量/函数)获得)
```
> 以下为添加break断点的实例(tbreak同理)
```
1.指定行号: break 10
2.指定文件行号: break test.cpp:10
3.指定函数: break fun
4.指定文件函数: break test.cpp:fun
5.指定条件: break 10 if flag == true
6.指定地址: 通过 info add main 得到地址 0x40148d,  break *0x40148d
```
> rbreak断点
> rbreak断点的添加方式是 rbreak + [正则表达式](http://www.runoob.com/regexp/regexp-syntax.html)
```
rbreak fun*   //给所有以fun开头的函数加断点
```
> 查看断点信息
```
info break 查看所有断点信息
info break breakpoint 查看第breakpoint个断点的信息
```
> 清除与管理断点
```
clean linenum 清除文件中linenum的断点
delete breakpoint 清除编号为breakpoint的断点
disable breakpoint1 禁止断点
enable breakpoint1 允许断点
```
<img src="/assert/debug/gdb/4.jpg" width="1230">
<br>
<h4>run&next</h4>

*参考至文献[ [9.](https://www.cnblogs.com/qigaohua/p/6077790.html)]*
> 程序执行分为运行和单步运行
```
1. run 运行准备调试的程序，在它后面可以跟随发给该程序的任何参数，包括标准输入和标准输出说明符(<和>)和shell通配符（*、？、[、]）在内。 如果你使用不带参数的run命令，gdb就再次使用你给予前一条run命令的参数，这是很有用的。
2. set args 修改发送给程序的参数
3. show args 查看其缺省参数的列表。
//单步执行
4. next 不进入的单步执行
5. step 进入的单步执行
6. finish 如果已经进入了某函数，而想退出该函数返回到它的调用函数中，可使用命令finish
7. until 结束当前循环
```
<img src="/assert/debug/gdb/5.jpg" width="1230">
<br>
<h4>print</h4>

>利用print命令可以检查各个变量的值, print 是 gdb 的一个功能很强的命令，利用它可以显示被调试的语言中任何有效的表达式。
```
print Var  打印出变量Var的值
print fun(x) 打印出函数fun(x)的值
print *obj 打印出某个数据结构或者对象
print $1 ($1为历史记录变量,在以后可以直接引用 $1 的值)
```
<br>
<h4>whatis</h4>

>查看变量类型
```
whatis Var 打印出Var的类型
```
<img src="/assert/debug/gdb/6.jpg" width="1230">
<br>
<h4> search </h4>

> search命令主要是查找文件中的串
```
search text 该命令可显示在当前文件中包含text串的下一行。
reverse-search text 该命令可以显示包含text 的前一行。
```
<img src="/assert/debug/gdb/7.jpg" width="1230">
<br>
<br>
[一篇很好的GDB调试命令总结](https://www.cnblogs.com/qigaohua/p/6077790.html)

------


<h4> 2. **GDB 调试实例** </h4>

下面的 ***test01.cpp*** 通过这个例子, 我们将学到关于GDB调试的基础命令

*参考至文献[ [2.](https://blog.csdn.net/haoel/article/details/2879)]*
<br>
```
//test01.cpp
#include <iostream>
#include <cstdio>


using namespace std;

int fun(int n){
    int sum = 0;
    for(int i = 0; i < n; ++i){
        sum += i;
    }
    return sum;
}

int main(){
    int i = 0;
    int result = 0;
    for(int i = 1; i <= 100; ++i){
        result += i;
    }

    cout << "result[1-100] = " << result << endl;
    cout << "result[1-200] = " << fun(200) << endl;
    return 0;
}

```
<br>
***GDB实例详解***
<br>
```
PS F:\Debugging\GDB> vim .\test01.cpp           --->> 创建文件并编辑
PS F:\Debugging\GDB> g++ -g -Wall .\test01.cpp -o test01.exe            --->> 编译
.\test01.cpp: In function 'int main()':
.\test01.cpp:16:9: warning: unused variable 'i' [-Wunused-variable]
     int i = 0;             --->> 输出警告信息
         ^
PS F:\Debugging\GDB> gdb .\test01.exe               --->> 进行gdb调试
GNU gdb (GDB) 7.6.1
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "mingw32".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from F:\Debugging\GDB\test01.exe...done.
(gdb) list                                  --->> list / l 列出程序代码
7       int fun(int n){
8           int sum = 0, i = 0;
9           for(i = 0; i < n; ++i){
10              sum += i;
11          }
12          return sum;
13      }
14
15      int main(){
16          int i = 0;
(gdb)                                       --->> 继续回车执行上一步的命令
17          int result = 0;
18          for(int i = 1; i <= 100; ++i){
19              result += i;
20          }
21
22          cout << "result[1-100] = " << result << endl;
23          cout << "result[1-200] = " << fun(200) << endl;
24          return 0;
25      }
(gdb) break 17                              --->> 在程序第17行设置断点
Breakpoint 1 at 0x4014b2: file .\test01.cpp, line 17.
(gdb) break fun                             --->> 对于fun函数设置断点
Breakpoint 2 at 0x401466: file .\test01.cpp, line 8.
(gdb) info break                            --->> 输出断点信息
Num     Type           Disp Enb Address    What
1       breakpoint     keep y   0x004014b2 in main() at .\test01.cpp:17
2       breakpoint     keep y   0x00401466 in fun(int) at .\test01.cpp:8
(gdb) run                                   --->> 运行程序
Starting program: F:\Debugging\GDB/.\test01.exe
[New Thread 14936.0x19a8]
[New Thread 14936.0x3a9c]
[New Thread 14936.0x28d8]

Breakpoint 1, main () at .\test01.cpp:17
17          int result = 0;
(gdb) n                                     --->> next / n 单步运行
18          for(int i = 1; i <= 100; ++i){
(gdb) n
19              result += i;
(gdb) n
18          for(int i = 1; i <= 100; ++i){
(gdb) c                                     --->> continue / c 继续运行
Continuing.
result[1-100] = 5050                        --->> 输出信息

Breakpoint 2, fun (n=200) at .\test01.cpp:8
8           int sum = 0, i = 0;
(gdb) print i                               --->> 打印i
$1 = 4201120
(gdb) n
9           for(i = 0; i < n; ++i){
(gdb) n
10              sum += i;
(gdb) print sum
$2 = 0
(gdb) n
9           for(i = 0; i < n; ++i){
(gdb) print sum
$3 = 0
(gdb) n
10              sum += i;
(gdb) n
9           for(i = 0; i < n; ++i){
(gdb) print sum                             --->> 打印sum
$4 = 1
(gdb) bt                                    --->> 输出栈信息
#0  fun (n=200) at .\test01.cpp:9   
#1  0x00401515 in _fu0___ZSt4cout () at .\test01.cpp:23
(gdb) finish                                --->> 结束函数
Run till exit from #0  fun (n=200) at .\test01.cpp:9
0x00401515 in _fu0___ZSt4cout () at .\test01.cpp:23
23          cout << "result[1-200] = " << fun(200) << endl;
Value returned is $5 = 19900
(gdb) c                                     --->> 继续运行
Continuing.
result[1-200] = 19900
[Inferior 1 (process 14936) exited normally]
(gdb) quit                                  --->> 运行结束, 退出gdb
PS F:\Debugging\GDB>
```
GDB调试的大致也就这么多, 灵活运用可以让让自己对程序的操作行云流水, 做到对自己的程序能随心所欲的控制.

<center>
<font color = pink>
**愿天堂无BUG**
</font>
</center>

### 参考文献
[1.] https://en.wikipedia.org/wiki/GNU_Debugger
[2.] https://blog.csdn.net/haoel/article/details/2879
[3.] https://sourceware.org/gdb/onlinedocs/gdb/
[4.] http://www.gnu.org/software/gdb/
[5.]http://wiki.ubuntu.org.cn/%E7%94%A8GDB%E8%B0%83%E8%AF%95%E7%A8%8B%E5%BA%8F
[6.] https://blog.csdn.net/fuqiangnxn/article/details/54140155
[7.] https://blog.csdn.net/sfeng177/article/details/53014289
[8.] https://blog.csdn.net/yangzhongxuan/article/details/6897968
[9.] https://www.cnblogs.com/qigaohua/p/6077790.html
