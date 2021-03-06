###练习4.1:
> 表达式5 + 10 * 20 / 2的求值结果是多少？

答：105

###练习4.2:
> 根据4.12节中的表，在下述表达式的合理位置添加括号，使得添加括号后运算对象的组合顺序与添加括号前一致。
```c++
(a) *vec.begin()		(b) *vec.begin() + 1
```

答：<br />
```c++
(a) *(vec.begin())		(b) (*(vec.begin())) + 1
```

###练习4.3:
> C++语言没有明确规定大多数二元运算符的求值顺序，给编译器优化留下了余地。这种策略实际上实在代码生成效率和程序潜在缺陷之间进行了权衡，你认为这可以接受吗？请说出你的理由。

答：可以接受，C++标准委员会应该只公布其标准，把其它实现的细节交给下面的编译器去实现，若C++语言把所有的细节都照顾到，那么存在不同的编译器又有什么意义呢？(个人理解，还请指正)。

###练习4.4:
> 在下面的表达式中添加括号，说明其求值的过程及最终结果，编写程序编译该(不加括号)表达式并输出其结果验证之前的推断。
```c++
12 / 3 * 4 + 5 * 15 + 21 % 4 / 2
```

答：<br />
```c++
((12 / 3) * 4) + (5 * 15) + ((21 % 4) / 2)
```

###练习4.5:
> 写出下列表达式的求值结果。
```c++
(a)-30 * 3 + 21 / 5	(b)-30 + 3 * 21 / 5
(c)30 / 3 * 21 % 5	(d)-30 / 3 * 21 % 4
```

答：<br />
```c++
(a)-86
(b)-18
(c)0
(d)-2
```

###练习4.6:
> 写出一条表达式用于确定一个整数是奇数还是偶数。

答：m % 2

###练习4.7:
> 溢出是何含义？写出三条将导致溢出的表达式。

答：当计算结果超出该类型所能表示的范围时就会产生溢出。<br />
```c++
INT_MAX + 1;LONG_MAX + 1;ULONG_MAX + 1;
```
注：必须包含头文件climits。参考：http://www.cplusplus.com/reference/climits/

###练习4.8:
> 说明在逻辑与、逻辑或及相等性运算符中运算对象的求值顺序。

答：<br />
逻辑与：当且仅当左侧运算对象为真时才对右侧运算对象求值。<br />
逻辑或：当且仅当左侧运算对象为假时才对右侧运算对象求值。<br />
相等性运算符：满足左结合律，按照从左向右的顺序求值。<br />

###练习4.9:
> 解释在下面的if语句中条件部分的判断过程。
```c++
 const char *cp = "Hello World";
 if(cp && * cp)
```

答：首先判断指针cp是否为空指针，当指针cp不为空的时候再判断cp所指向的对象的第一个字符是否为空。

###练习4.10:
> 为while循环写一个条件，使其从标准输入中读取整数，遇到42时停止。

答：<br />
```c++
int num;
while(cin >> num && num != 42)
```

###练习4.11:
> 书写一条表达式用于测试4个值a、b、c、d的关系，确保a大于b、b大于c、c大于d。

答:<br />
```c++
if(a > b && b > c && c > d)
```

###练习4.12:
> 假设i、j和k是三个整数，说明表达式i != j < k的含义。

答：查表4.12可知，"<"运算符的优先级高于"!="运算符。所以该表达式的含义是：先判断j < k，然后再与i进行运算，等价与(i != (j < k))。

###练习4.13:
> 在下述语句中，当赋值完成后i和d的值分别是多少？
```c++
 int i; double d;
 (a)d = i = 3.5;	(b)i = d = 3.5
```

答：<br />
```c++
(a)i = 3, d = 3
(b)i = 3, d = 3.5
```

###练习4.14:
> 执行下述if语句后将发生什么情况？
```c++
 if(42 = i) // ...
 if(i = 42) // ...
```

答：第一条语句将会产生编译错误，赋值运算符的左侧运算对象必须是一个可修改的左值，而字面值是右值。<br />
第二条语句判断正确，接着执行if语句后面的语句。

###练习4.15:
> 下面的赋值是非法的，为什么？应该如何修改？
```c++
 double dval; int ival; int *pi;
 dval = ival = pi = 0;
```

答：对于多重赋值语句中的每一个对象，它的类型或者与右边对象的类型相同、或者可由右边对象的类型转换得到。pi和ival的类型不同，但是pi的类型(int*)无法转换成ival的类型(int)，所以尽管0这个值能赋给任何对象，但是该赋值语句仍然是非法的。应修改为dval = ival = *pi = 0。

###练习4.16:
> 尽管下面的语句合法，但它们实际执行的行为可能和预期并不一样，为什么？应该如何修改？
```c++
 (a)if(p = getPtr() != 0)	(b)if(i = 1024)
```

答：<br />
(a)赋值运算符的优先级低于关系运算符的优先级，所以在条件语句中，赋值运算符部分通常应该加上括号。应修改为if((p = getPtr()) != 0)<br />
(b)C++语言允许用赋值运算作为条件，但是这一特性可能带来意想不到的后果。该if语句把字面值1024赋给了i，然后检查赋值的结果是否为真。如果i不为0,则条件为真。应修改为if(i == 1024)。<br />

###练习4.17:
> 说明前置递增运算符和后置递增运算符的区别。

答：前置版本将对象本身作为左值返回，后置版本则将对象原始值的副本作为右值返回。

###练习4.18:
> 如果第132页那个输出vector对象元素的while循环使用前置递增运算符，将得到什么结果？

答：解引用该值将产生错误的结果。不但无法正确输出第一个元素，而且更糟糕的是如果序列中没有负值，程序将可能试图解引用一个根本不存在的元素。

###练习4.19:
> 假设ptr的类型是指向int的指针、vec的类型是vector<int>、ival的类型是int，说明下面的表达式是何含义？如果有表达式不正确，为什么？应该如何修改？
```c++
 (a)ptr != 0 && *ptr++	(b)ival++ && ival
 (c)vec[ival++] <= vec[ival]
```

答：<br />
(a)判断ptr是否为空指针，若不为空指针，再判断ptr所指向的值是否为0,然后将ptr指向下一位置。<br />
(b)判断ival是否为0,然后把ival的值加1,若ival的值不为0,再判断加1后的值是否为0。<br />
(c)vec[ival]的值和vec[ival+1]的值的大小，等价与vec[ival] <= vec[ival+1]
感觉条件不足，无法判断表达式正确与否。<br />

###练习4.20:
> 假设iter的类型是vector<string>::iterator,说明下面的表达式是否合法。如果合法，表达式的含义是什么？如果不合法，错在何处？
```c++
(a)*iter++;	(b)(*iter)++;	(c)*iter.empty();
(d)iter->empty();(e)++*iter;	(f)iter++->empty();
```

答：<br />
(a)合法，解引用iter所指向的string，并将iter移动到下一位置。<br />
(b)不合法，解引用iter以后的结果是string，然后将string执行后置递增操作。<br />
(c)不合法，解引用运算符的优先级低于点运算符，而iter没有名为empty的成员。<br />
(d)合法，运行iter所指对象的empty成员。<br />
(e)不合法，理由同(b)<br />
(f)合法，先执行iter的empty成员，然后将iter移动到下一位置。<br />

###练习4.21:
> 编写一段程序，使用条件运算符从vector<int>中找到哪些元素的值是奇数，然后将这些奇数值翻倍。

答：<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
 vector<int> ivec;
 for(int i = 0;i != 10;++i)
  ivec.push_back(i);
 for(auto i : ivec)
  cout << i << " ";
 cout << endl;
 for(auto i : ivec)
 {
   i % 2?i *= 2:i;
   cout << i << " ";
 }
  cout << endl;
 return 0;
}
```

###练习4.22:
> 本节的示例程序将成绩划分成high pass、pass和fail三种，扩展该程序使进一步将60分到75分之间的成绩设定为low pass。要求程序包含两个版本:一个版本只使用条件运算符：另外一个版本使用1个或多个if语句。哪个版本的程序更容易理解呢？为什么？

答：<br />
```c++
finalgrade = (grade > 90)?"high pass":(grade < 60)?"fail":(grade < 75)?"low pass":"pass"
if(grade > 90)
 finalgrade = "high pass";
if(grade > 60 && grade < 75)
 finalgrade = "low pass";
if(grade < 60)
 finalgrade = "fail";
```

第二种版本更容易理解一些，因为随着条件运算符嵌套层数的增加，代码的可读性急剧下降。因此，条件运算的嵌套最好别超过两到三层。

###练习4.23:
> 因为运算符的优先级问题，下面这条表达式无法通过编译。根据4.12节中的表(第147页)指出它的问题在哪里？应该如何修改？？
```c++
string s = "word";
string p1 = s + s[s.size() - 1] == 's'?"":"s";
```

答：因为加法运算符的优先级高于相等运算符的优先级高于条件运算符的优先级，所以原表达式等于((s + (s[s.size() - 1])) == 's')?"":"s"，应修改为s + (((s[s.size() - 1]) == 's')?"":"s")

###练习4.24:
> 本节的示例程序将成绩划分为high pass、pass和fail三种，它的依据是条件运算符满足右结合律。假如条件运算符满足的是左结合律，求值过程将是怎样的？

答：按照从左向右的顺序结合，将会出现错误，因为条件运算符的两个表达式类型不同，一个是const char * ,另一个是bool，试着加括号改变结合顺序：
```c++
finalgrade = ((grade > 90)?"high pass":(grade < 60))?"fail":"pass";
```
将会报错：
```c++
error: operands to ?: have different types ‘const char*’ and ‘bool’
   finalgrade = ((grade > 90)?"high pass":(grade < 60))?"fail":"pass"; 
                                                     ^
```
###练习4.25:
> 如果一台机器上int占32位、char占8位，用的是Latin-1字符集，其中字符'q'的二进制形式是01110001,那么表达式~'q' << 6的值是什么？

答：<br />
```c++
0000 0000 0000 0000 0010 0011 1000 0000
```

###练习4.26:
> 在本节关于测验成绩的例子中，如果使用unsigned int作为quiz1的类型会发生什么情况？

答：int类型只能确保占有16位，因为班中至少有30名学生，所以移位时将会产生未定义的行为。

###练习4.27:
> 下列表达式的结果是什么？
```c++
unsigned long ul1 = 3,ul2 = 7;
(a)ul1 & ul2	(b)ul1 | ul2
(c)ul1 && ul2	(d)ul1 || ul2
```

答：<br />
```c++
(a)3		(b)7
(c)true		(d)true
```

###练习4.28:
> 编写一段程序，输出每一种内置类型所占空间的大小。

答：以int为例，其它类似。
```c++
#include<iostream>
using namespace std;
int main()
{
 cout << "int:\t" << sizeof(int) << endl;
 return 0;
}
```

###练习4.29:
> 推断下面代码的输出结果并说明理由。实际运行这段程序，结果和你想的一样吗？如果不一样，为什么？
```c++
int x[10]; int *p = x;
cout << sizeof(x)/sizeof(*x) << endl;
cout << sizeof(p)/sizeof(*p) << endl;
```

答：输出
```c++
10
2
```

对数组执行sizeof运算得到整个数组所占空间的大小，等价于对数组中所有元素各执行以此sizeof运算并将所得结果求和，sizeof(*x)既x[0]的大小，两者之商即为数组的大小; * p指向int，大小为4,p的类型为int*，我所在的环境为64位，所以占8位，两者之商为2。

###练习4.30:
> 根据4.12节中的表(第147页)，在下述表达式的适当位置加上括号，使得加上括号之后表达式的含义与原来的含义相同。
```c++
(a)sizeof x + y		(b)sizeof p->mem[i]
(c)sizeof a < b		(d)sizeof f()
```

答：
```c++
(a)sizeof(x) + y	(b)sizeof(p->mem[i])
(c)sizeof(a) < b	(d)sizeof(f())
```

###练习4.31:
> 本节的程序使用了前置版本的递增运算符和递减运算符，解释为什么要用前置版本而不用后置版本。要想使用后置版本的递增递减运算符需要做哪些改动？使用后置版本重写本节的程序。

答：<br />
前置版本将对象本身作为左值返回，后置版本则将对象原始值的副本作为右值返回。在此处本身并没有什么区别，所以并不需要什么改动。<br />
参考：<br />
(1)http://stackoverflow.com/questions/22591387/usage-of-the-built-in-comma-operator<br />
(2)http://www.zhihu.com/question/24484761<br />
(3)http://bbs.csdn.net/topics/390846064<br />

###练习4.32:
> 解释下面这个循环的含义。
 ```c++
 constexpr int size = 5;
 int ia[size] = {1,2,3,4,5};
 for(int *ptr = ia,ix = 0;
  ix != size && ptr != ia + size;
  ++ix,++ptr) { /* ... */ }
```

答：遍历数组中的各个元素。

###练习4.33:
> 根据4.12节中的表(第147页)说明下面这条表达式的含义。
```c++
 someValue ? ++x, ++y : --x, --y
```

答：因为逗号运算符的优先级最低，所以该表达式等价于:
```c++
(someValue ? ++x, ++y : --x), --y
```

当someValue为真是执行++x,++y,--y,然后返回y的值，当somevalue为假时执行--x,--y,返回y的值。<br />
参考：<br />
(1)http://www.zhihu.com/question/27214955<br />
(2)https://github.com/pezy/Cpp-Primer/tree/master/ch04#exercise-433<br />
(3)https://github.com/pezy/Cpp-Primer/tree/master/ch04#exercise-433<br />

###练习4.34:
> 根据本节给出的变量定义，说明在下面的表达式中将发生什么样的类型转换：
```c++
(a)if(fval)	(b)dval = fval + ival;	(c)dval + ival * cval;
```

答：<br />
(a)fval转换成bool。<br />
(b)ival转换成float，相加的结果再转换为double。<br />
(c)cval提升为int，与ival的乘积转换为double，然后与dval相加。<br />

###练习4.35:
> 假设有如下定义，
```c++
 char cval;	int ival;	unsigned int ui;
 float fval;	double dval;
```

> 请回答在下面的表达式中发生了隐式类型转换吗？如果有，指出来。
```c++
 (a)cval = 'a' + 3;	(b)fval = ui -ival * 1.0;
 (c)dval = ui * fval	(d)cval = ival + fval + dval;
```

答：<br />
(a)'a'提升成int，然后与3相加，结果转换成char。<br />
(b)ival转换成double，然后与1.0相乘，ui转换成double，相减的结果转换成float赋值给fval。<br />
(c)ui转换成float，与fval相乘的结果转换成double，然后赋值给dval。<br />
(d)ival转换成float与fval相加，结果转换成double与dval相加，最后转换成char赋值给cval。<br />

###练习4.36:
> 假设i是int类型，d是double类型，书写表达式i *= d使其执行整数类型的乘法而非浮点类型的乘法。

答：i *= static_cast<int>(d)

###练习4.37:
> 用命名的强制类型转换改写下列旧式的转换语句。
```c++
int i; double d; const string *ps; char *pc; void *pv;
(a)pv = (void*)ps;	(b)i = int(*pc);
(c)pv = &d;		(d)pc = (char*)pv;
```

答：<br />
```c++
(a)pv = const_cast<void*>ps;	(b)i = static_cast<int>(*pc);
(c)pv = static_cast<void*>(&d)	(d)pc = static_cast<char*>(pv);
```

###练习4.38:
> 说明下面这条表达式的含义。
```c++
 double slope = static_cast<double>(j/i);
```

答：j与i相除的结果用命名的强制类型转换为double。


