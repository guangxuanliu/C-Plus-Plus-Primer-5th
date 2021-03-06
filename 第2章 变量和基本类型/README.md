###练习2.1:
>类型int、long、long long和short的区别是什么？无符号类型和带符号类型的区别是什么？float和double的区别是什么？

答：在我的编译环境中，int占4字节，long占8字节，long long占8字节。无符号和带符号所表示的范围不同，如signed char理论上可以表示-127到127，unnsigned char表示0到256。float占4个字节，double占8个字节，切double比float精度高，一般应使用double。

###练习2.2:
> 计算按揭贷款时，对于利率、本金和付款分别应选择何种数据类型？说明你的理由。

答：缺少这方面的社会经验，结合实际情况选择。

###练习2.3:
> 读程序写结果。
```c++
unsigned u = 10,u2 = 42;
std::cout << u2 - u << std::endl;
std::cout << u - u2 << std::endl;
int i = 10,i2 = 42;
std::cout << i2 - i << std::endl;
std::cout << i - i2 << std::endl;
std::cout << i - u << std::endl;
std::cout << u - i << std::endl;
```

答:
结果依次是：
```c++
32
4294967264
32
-32
0
0
```

###练习2.4:
> 编写程序检查你的估计是否正确，如果不正确，请仔细研读本节直到弄明白问题所在。

答：见上一题。

###练习2.5:
> 指出下述字面值的数据类型并说明每一组内几种字面值的区别：
```c++
(a) 'a', L'a', "a", L"a"
(b) 10, 10u, 10L, 10uL, 012, 0xC
(c) 3.14, 3.14f, 3.14L
(d) 10, 10u, 10., 10e-2
```

答：<br />
(a)字符，宽字符，字符串，宽字符串<br />
(b)整型，无符号整型，长整型，无符号长整型，八进制，十六进制<br />
(c)双精度浮点型，单精度浮点型，扩展精度浮点型<br />
(d)整型，无符号整型，双精度浮点型，双精度浮点型

###练习2.6:
> 下面两组定义是否有区别，如果有，请叙述之：
```c++
int month = 9, day = 7;
int month = 09, day = 07;
```

答：有区别，第一组是十进制，第二组是八进制。但是无“09”对应的八进制。

###练习2.7:
> 下述字面值表示何种含义？它们各自的数据类型是什么？
```c++
(a) "Who goes with F\145rgus?\012"
(b) 3.14e1L
(c) 1024f
(d) 3.14L
```

答：<br />
(a)\145是字母‘e’，\012是换行符。字符串类型<br />
(b)表示3.14。扩展精度类型。<br />
(c)什么都不代表，编译不通过。
参考：[Stackoverflow](http://stackoverflow.com/questions/28316769/1024f-invalid-suffix-f-on-integer-constant)<br />
(d)代表3.14，扩展精度类型。

###练习2.8:
> 请利用转移序列编写一段程序，要求先输出2M，然后转到新一行。修改程序使其先输出2，然后输出制表符，在输出M，最后转到新一行。

答：
```c++
(1)cout << 2 << '\115' << '\n';
(2)cout << 2 << '\t' << '\115' << '\n';
```

###练习2.9:
> 解释下列定义的含义。对于非法的定义，请说明错再何处并将其改正。
```c++
(a) std::cin >> int input_value;
(b) int i = {3.14};
(c) double salary = wage = 9999.99;
(d) int i = 3.14;
```

答：<br />
(a)非法，此处不能声明变量，应该先定义再使用。<br />
(b)合法，但是会有警告信息。(按作者的意思应该是不合法，作者在书中用了‘错误’两个字)<br />
```c++
warning: narrowing conversion of ‘3.1400000000000001e+0’ from ‘double’ to ‘int’ inside { } [-Wnarrowing]
  int i = {3.14};
               ^
```

(c)不合法，wage没有定义，应先定义wage再使用。
(d)合法，不给出警告，但是信息会丢失。

###练习2.10:
> 下列变量的初值分别是什么？
```c++
std::string global_str;
int global_int;
int main()
{
  int local_int;
  std::string local_str;
}
```

答：global_str和local_str的初始值为空串，global_int和local_int的初始值为0 。(按作者的意思，global_str和local_str的初始化方式由std::string决定，即初始化为空串，global_int定义在函数外，被默认初始化为0，local_int定义在函数内，其值是未定义的)
。

###练习2.11:
> 指出下面的语句是声明还是定义：
```c++
(a)extern int ix = 1024;
(b)int iy;
(c)extern int iz;
```

答：<br />
(a)定义，如果在函数体内部的话会报错。<br />
(b)声明并定义。<br />
(c)声明。

###练习2.12:
> 请指出下面的名字中哪些是非法的？
```c++
(a) int double = 3.14
(b) int _;
(c) int catch-22;
(d) int 1_or_2 = 1;
(e) double Double = 3.14;
```

答：<br />
(a)非法，使用了关键字。<br />
(b)合法。<br />
(c)非法，标识符由字母、数字、下划线组成。<br />
(d)非法，标识符不应该以数字开头。<br />
(e)合法。

###练习2.13:
> 下面程序中j的值是多少？
```c++
int i = 42;
int main()
{
 int i = 100;
 int j = i;
}
```

答：100 。

###练习2.14:
> 下面的程序合法嘛？如果合法，它将输出什么？
```c++
int i = 100, sum = 0;
for (int i = 0; i != 10; ++i)
 sum += i;
std::cout << i << " " << sum << std::endl;
```

答：合法。输出：'100' '45' 。

###练习2.15:
> 下面那个定义是不合法的？为什么？
```c++
(a) int ival = 1.01;
(b) int &rval1 = 1.01;
(c) int &rval2 = ival;
(d) int &rval3;
```

答：<br />
(a)合法，舍去小数部分。<br />
(b)不合法，必须用对象去初始化引用。<br />
(c)合法。<br />
(d)不合法，引用必须初始化。

###练习2.16:
> 考查下面的所有赋值然后回答：哪些赋值是不合法的？为什么？哪些赋值是合法的？它们执行了什么样的操作？
```c++
int i = 0, &r1 = i; double d = 0, &r2 = d;
(a) r2 = 3.14159;
(b) r2 = r1;
(c) i = r2;
(d) r1 = d;
```

答：<br />
(a)合法，把3.14159赋值给了d。<br />
(b)合法，把i的值赋给了d。<br />
(c)合法，把d的值赋给了i。<br />
(d)合法，把d的值赋给了i。

###练习2.17:
> 执行下面的代码段将输出什么结果？
```c++
int i, &ri = i;
i = 5;ri = 10;
std::cout << i << " " << ri << std::endl;
```

答：10 10。

###练习2.18:
> 编写代码分别更改指针的值以及指针所指对象的值。

答:
```c++
#include<iostream> 
int main() 
{ 
 int val1 = 10,val2 = 20; 
 int *p = &val1; 
 std::cout << p << std::endl; 
 std::cout << *p << std::endl; 
 p = &val2; 
 *p = 30; 
 std::cout << p << std::endl; 
 std::cout << *p << std::endl; 
 return 0; 
}
```

###练习2.19:
> 说明指针和引用的主要区别。

答：<br />
* 1.指针本身就是一个对象，允许对指针赋值和拷贝，而且在指针的生命周期内它可以先后指向几个不同的对象。<br />
* 2.指针无须在定义时赋初值。

###练习2.20:
> 请叙述下面这段代码的作用。
```c++
int i = 42;
int *p1 = &i;
*p1 = *p1 * *p1;
```

答：该代码实现了i的平方。

###练习2.21:
> 请解释下述定义。在这些定义中有非法的吗？如果有，为什么？
```c++
int i = 0;
(a) double* dp = &i;
(b) int *ip = i;
(c) int *p = &i;
```

答：<br />
(a)非法。把int型对象的地址赋给double型指针。<br />
(b)非法。不能把int型变量直接赋给指针。<br />
(c)合法。<br />

###练习2.22:
> 假设p是一个int型指针，请说明下述代码的含义。
```c++
if(p) //...
if(*p) //...
```

答：第一个判断指针是否为空；第二个判断指针所指向的对象是否为0。

###练习2.23:
> 给定指针p，你能知道它是否指向了一个合法的对象吗？如果能，叙述判断思路；如果不能，也请说明原因。

答：可以对指针进行解引用进行一些操作，如果无错误则说明指向一个合法的对象。再一个就是根据个人经验判断是否在所使用系统中可访问地址之内来判断是否指向合法对象。

###练习2.24:
> 再下面这段代码中为什么p合法而lp非法？
```c++
int i = 42;
void *p = &i;
long *lp = &i;
```

答：void * 是一种特殊的指针类型，可用于存放任意对象的地址，所以p合法。而lp是long int类型的指针，用int型对象的指针初始化是非法的。

###练习2.25:
> 说明下列变量的类型和值。
```c++
(a) int* ip,i,&r = i;
(b) int i,*ip = 0;
(c) int* ip,ip2;
```

答：<br />
(a)ip是指向int型的指针，值为nullptr;i为int型，值为0;r为指向int型指针的引用。<br />
(b)i为int型，值为0；ip为指向int型的指针，值为nullptr。<br />
(c)ip为指向int型的指针，值为nullptr；ip2为int型，值为0。

###练习2.26:
> 下面哪些句子是合法的？如果有不合法的句子，请说明为什么？
```c++
(a) const int buf;
(b) int cnt = 0;
(c) const int sz = cnt;
(d) ++cnt; ++sz;
```

答：<br />
(a)不合法，const对象定义时必须初始化。<br />
(b)合法。<br />
(c)合法。<br />
(d)不合法，const对象的值不可以改变。

###练习2.27:
> 下面的哪些初始化是合法的？请说明原因。
```c++
(a) int i = -1, &r = 0;
(b) int *const p2 = &i2;
(c) const int i = -1, &r = 0;
(d) const int *const p3 = &i2;
(e) const int *p1 = &i2;
(f) const int &const r2;
(g) const int i2 = i, &r = i;
```

答：<br />
(a)不合法，引用只能绑定到对象上，而不能与字面值或某个表达式的计算结果绑定在一起。<br />
(b)合法。<br />
(c)合法。初始化常量引用时允许用任意表达式作为初始值。<br />
(d)合法。<br />
(e)合法。<br />
(f)不合法，const对象一旦创建后其值就不能改变，所以const对象必须初始化，而且没有这种写法。<br />
(g)合法。 

###练习2.28:
> 说明下面的这些定义是什么意思，挑出其中不合法的。
```c++
(a) int i, *const cp;
(b) int *p1, *const p2;
(c) const int ic, &r = ic;
(d) const int *const p3;
(e) const int *p;
```

答：<br />
(a)不合法，const对象必须初始化。<br />
(b)不合法，const对象必须初始化。<br />
(c)不合法，const对象必须初始化。<br />
(d)不合法，const对象必须初始化。<br />
(e)不合法，const对象必须初始化。

###练习2.29:
> 假设已有上一练习中定义的那些变量，则下面的哪些语句是合法的？请说明原因。
```c++
(a) i = ic;
(b) p1 = p3;
(c) p1 = &ic;
(d) p3 = &ic;
(e) p2 = p1;
(f) ic = *p3;
```

答：<br />
(a)合法，利用一个对象去初始化另一个对象，它们是不是const都无关紧要。<br />
(b)合法。<br />
(c)不合法，类型不一致。<br />
(d)合法。<br />
(e)合法。<br />
(f)合法。

###练习2.30:
> 对于下面的这些语句，请说明对象被声明成了顶层const还是底层const？
```c++
const int v2 = 0;
int v1 = v2;
int *p1 = &v1, &r1 = v1;
const int *p2 = &v2, *const p3 = &i, &r2 = v2;
```

答：v2为顶层const；p2为底层const；p3为顶层const。

###练习2.31:
> 假设已有上一个练习中所做的那些声明，则下面的那些语句是合法的？请说明顶层const和底层const在每个例子中有何体现。
```c++
r1 = v2;
p1 = p2; p2 = p1;
p1 = p3; p2 = p3;
```

答：<br />
r1 = v2非法。<br />
p1 = p2非法。<br />
p2 = p1合法。<br />
p1 = p3非法。<br />
p2 = p3合法。<br />
原因：当执行对象的拷贝操作时，顶层const不受什么影响，底层const的限制不能忽视。拷入和拷出的对象必须具有相同的底层const资格，或者两个对象的数据类型必须能够转换。

###练习2.32:
> 下面的代码是否合法？如果非法，请设法将其修改正确。
```c++
int null = 0, *p = null;
```

答：非法，将一个整型变量赋值给整型指针。
改为'*p = nullptr'或者'*p = &null'。

###练习2.33:
> 利用本节定义的变量，判断下列语句的运行结果。
```c++
a = 42; b = 42; c = 42;
d = 42; e = 42; g = 42;
```

答：<br />
a,b,c为整型，所以可以赋值，结果为42。<br />
d是整型指针，直接赋值字面值是非法的。<br />
e是指向整型常量的指针，直接赋值字面值是非法的。<br />
g为整型常量的引用，不合法。

###练习2.34:
> 基于上一个练习中的变量和语句编写一段程序，输出赋值前后变量的内容，你刚才判断正确吗？如果不对，请反复研读本节的示例直到你明白错在何处为止。
```c++
#include <iostream>
int main()
{
 int i = 0, &r = i;
 auto a = r;
 const int ci = i, &cr = ci;
 auto b = ci;
 auto c = cr;
 auto d = &i;
 auto e = &ci;
 const auto f = ci;
 auto &g = ci;
 a = 42;
 b = 42;
 c = 42;
 d = 42;
 e = 42;
 g = 42;
 return 0;
}
```

###练习2.35:
> 判断下列定义推断出的类型是什么，然后编写程序进行验证。

```c++
const int i = 42;
auto j = i; const auto &k = i; auto *p = &i;
const auto j2 = i, &k2 = i;
```

答：j为int；k为const int&；p为const int * ；j2为const int；k2为const int&。

###练习2.26:
> 关于下面的代码，请指出每个变量的类型以及程序结束时他们的值。
```c++
int a = 3, b = 4;
decltype(a) c = a;
decltype((b)) d = a;
++c;
++d;
```

答：<br />
a是int型，值为4 。<br />
b是int型，值为4 。<br />
c是int型，值为4 。<br />
d是int&，值为4 。

###练习2.37:
> 赋值是会产生引用的一类典型表达式，引用的类型就是左值的类型。也就是说，如果i是int，则表达式i = x的类型是int& 。根据这一特点，请指出下面代码中每一个变量的类型和值。
```c++
int a = 3, b = 4;
decltype(a) c = a;
decltype(a = b) d = a;
```

答：<br />
a是int型，值为3 。<br />
b是int型，值为4 。<br />
c是int型，值为3 。<br />
d是int& ，值为3 。

###练习2.38:
> 说明由decltype指定类型和由auto指定类型有何区别。请举出一个例子，decltype指定的类型与auto指定的类型一样；再聚一个例子，decltype指定的类型与auto指定的类型不一样。

答：<br />
auto：当初始值为引用时，编译器会以引用对象的类型作为auto的类型；一般会忽略掉顶层const。<br />
decltype：如果使用的表达式是一个变量，则decltype返回该变量的类型(包括顶层const和引用在内)；如果使用的表达式不是一个变量，返回表达式结果对应类型。

```c++
decltype(f()) sum1 = f();
auto sum2 = f();

const int i = 20;
const int &ri = i;
decltype(ri) dri1 = i;
auto dri2 = ri;
```

###练习2.39:
> 编译下面的程序观察其运行结果，注意，如果忘记写类定义体后面的分号会发生什么情况？记录下相关信息，以后可能会有用。
```c++
struct Foo { /* 此处为空 */ } //注意：没有分号
int main()
{
 return 0;
}
```

答：<br />
```c++
error: expected ‘;’ after struct definition
 struct Foo {}
             ^
```
###练习2.40:
> 根据自己的理解写出Sales_data类，最好与书中的例子有所区别。

答：按书中的来就行，以防后面再出Sales_data类的问题代码不统一。
```c++
struct Sales_data 
{
 std::string bookNo;
 unsigned units_sole = 0;
 double revenue = 0.0;
}
```

###练习2.41:
> 使用你自己的Sales_data类重写1.5.1节(第20页)、1.5.2节(第21页)和1.6节(第22页)的练习。眼下先把Sales_data类的定义和main函数放在一个文件里。

答：Sales_data类的定义可以参考书中的代码。

###练习2.42:
> 根据你自己的理解重写一个Sales_data.h头文件，并以此为基础重做2.6.2(第67页)的练习。

答：可以参考书中的代码。
