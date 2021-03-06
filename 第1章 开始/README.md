###练习 1.1:
> 查阅你使用的编译器的文档，确定它所使用的文件命名约定。编译并运行第２页的main程序。

答：我使用的编译器是GCC 4.8.2,官方文档可以在gcc.gnu.org/onlinedocs中查阅。

###练习 1.2:
> 改写程序，让它返回-1。返回值-1通常被当做程序错误的标识。重新编译运行你的程序，观察你的系统如何处理main返回的错误标识。

答：使用g++ xx.cpp编译程序的时候没有什么特殊提示，和返回0没什么区别。此处问题所说的“如何处理”肯定不是这个意思，我理解有误，以后再回过头来看看。

###练习 1.3:编写程序,在标准输出上打印Hello,World.
```c++ 
#include<iostream>
int main()
{
 std::cout << "Hello,World" << std::endl;
 return 0;
}
```

###练习1.4:
> 我们的程序使用加法运算符+来将两个数相加。编写程序使用乘法运算符 * ，来打印两个数的积。

```c++
#include<iostream>
int main()
{
 std::cout << "Enter two numbers:" << std::endl;
 int v1 = 0,v2 = 0;
 std::cin >> v1 >> v2;
 std::cout << "The product of" << v1 << " and " << v2
	   << " is " << v1 * v2 << std::endl;
return 0;
}
```

###练习1.5:
> 我们将所以输出操作放在一条很长的语句中。重写程序，将每个运算对象的打印操作放在一条独立的语句中。

```c++
#include<iostream>
int main()
{
 std::cout << "Enter two numbers:";
 std::cout << std::endl;
 int v1 = 0,v2 = 0;
 std::cin >> v1 >> v2;
 std::cout << "The sum of ";
 std::cout << v1;
 std::cout << " and ";
 std::cout << v2;
 std::cout << " is ";
 std::cout << v1 * v2;
 std::cout << std::endl;
 return 0;
}
```

###练习1.6:
> 解释下面程序设计片段是否合法。
 ```c++
std::cout << "The sum of " << v1;
	   << " and " << v2;
	   << " is " << v1 + v2 << std:: endl;
```
如果程序是合法的，它输出什么？如果程序不合法，原因何在？应该如何修正？

答：不合法。<<运算符接受两个运算对象：左侧的运算对象必须是一个ostream对象，右侧的运算对象是要打印的值。后两行均缺少左侧运算对象。两种修改方案，第一种如书中的示例；第二种在后两行开头分别加上std::cout

###练习1.7:
> 编译一个包含不正确的嵌套注释的程序，观察编译器返回的错误信息。

答:
```c++
#include<iostream>
/*  
 *注释对/* */不能嵌套。
 *“不能嵌套”几个字会被认为是源码，
 *像剩余程序一样处理
 */

int main()
{
 return 0;
}
```

编译器不同，给出的错误信息也不同，我的是
```c++
main.cpp:3:17: error: stray ‘\XXX’ in program
```

###练习1.8:
>指出下列哪些输出语句是合法的(如果有的话)
```c++
 std::cout << "/*";
 std::cout << "*/";
 std::cout << /* "*/" */;
 std::cout << /* "*/"/* "/*" */;
```
预测编译这些语句会产生什么样的结果，实际编译这些语句来验证你的答案(编写一个小程序，每次将上述一条语句作为其主题)，改正每个编译错误。

答：第三条语句报错：
```c++
main.cpp:4:20: warning: missing terminating " character [enabled by default]
 std::cout << /* "*/" */;
                    ^
```
其他都正确。

###练习1.9:
> 编写程序，使用while循环将50到100的整数相加。

答:
```c++
#include<iostream>
int main()
{
 int sum = 0,val = 50;
 while(val <= 100)
 {
  sum += val;
  ++val;
 }
 std::cout << "Sum of 50 to 100 inclusive is " << sum << std::endl;
 return 0;
}
```

###练习1.10:
> 除了++运算符将运算对象的值增加1之外，还有一个递减运算符(--)实现将值减少1，编写程序，使用递减运算符在循环中按递减顺序打印出10到0之间的整数。

答:
```c++
#include<iostream>
int main()
{
 int val = 10;
 while(val >= 0)
 {
  std::cout << val << std::endl;
  --val;
 }
 return 0;
}
```

###练习1.11:
> 编写程序，提示用户输入两个整数，打印出这两个整数所指定范围内的所有整数。

答:
```c++
#include<iostream>
int main()
{
 int val1 = 0,val2 = 0;
 std::cout << "Please enter two number:" << std::endl;
 std::cin >> val1 >> val2;
 if(val2 < val1)
 {
  int temp = val1;
  val1 = val2;
  val2 = temp;
 }
 while(val1 <= val2)
 {
  std::cout << val1 << std::endl;
  ++val1;
 }
return 0;
}
```

###练习1.12:
> 下面的for循环完成了什么功能？sum的终值是多少？
```c++
 int sum = 0;
 for(int i = -100;i <= 100;++i)
  sum += i;
```

答：该循环从计算了从-100到100的和。sum的结果是0。

###练习1.13:
> 使用for循环重做1.4.1节中的所有练习(第11页)。

答：将while循环替换为下面的for循环即可。
```c++
 int sum = 0;
 for(int val = 50;val <= 100;++val)
  sum += val;

 for(int val = 10;val >= 0;--val)
  std::cout << val << std::endl;

 for(;val1 <= val2;++val1)
  std::cout << val1 << std::endl;
```

###练习1.14:
> 对比for循环和while循环，两种形式的优缺点各是什么？

答：
在for循环中，循环控制变量的初始化和修改都放在语句头部分，形式较简洁，且特别适用于循环次数已知的情况。<br />
在while循环中，循环控制变量的初始化一般放在while语句之前，循环控制变量的修改一般放在循环体中，形式上不如for语句简洁，但它比较适用于循环次数不易预知的情况（用某一条件控制循环）。<br />
两种形式各有优点，但它们在功能上是等价的，可以相互转换。

###练习1.15:
> 编写程序，包含第14页“再探编译”中讨论的常见错误，熟悉编译器生成的错误信息。

答：编译器不同，错误信息不同，根据自己所用的编译器看一下错误信息。

###练习1.16:
> 编写程序，从cin读取一组数，输出其和。

答：
```c++
/*
 *输入数据后输入文件结束符结束输入
 *Windows系统中为Ctrl+Z
 *Unix系统中为Ctrl+D
 */

#include<iostream>
int main()
{
 int sum = 0,val = 0;
 std::cout << "Please enter a serial of numbers:" << std::endl;
 while(std::cin >> val)
  sum += val;
 std::cout << std:: endl << "Sum is: " << sum << std::endl;
 return 0; 
}

/*
 *该程序不用输入文件结束符
 *输入结束后按回车即可
 */
#include<iostream>
int main()
{
 int sum = 0,val = 0;
 std::cout << "Please enter a serial of numbers:" << std::endl;
 while(std::cin >> val && std::cin.get() != '\n')
  sum += val;
 std::cout << "Sum is: " << sum << std::endl;
 return 0; 
}
```

###练习1.17:
> 如果输入的所有值都是相等的，本节的程序会输出什么？如果没有重复值，输出又会是怎样的？

答：如果所有的输入都相等，会只输出一行，某个数出现了多少次。
如果没有重复值，那么每个数出现一行，并显示出现一次。

###练习1.18:
> 编译并运行本节的程序，给它输入全都相等的值。再次运行程序，输入没有重复的值。

答：此题还得回看，有不清楚的地方。按照作者的输入，必须再次按下Ctrl+D才会出现最后一个。<br />
问题已得到解答，第一个Ctrl+D并没有产生EOF，第二个才是文件结束符。参见:[Stackoverflow](http://stackoverflow.com/questions/28289534/c-primer-5th-1-4-4/28290350#28290350)

###练习1.19:
> 修改你为1.4.1节练习1.10(第11页)所编写的程序(打印一个范围内的数)，使其能处理用户输入的第一个数比第二个数小的情况。

答：参见练习1.11,已经加入了处理大小数的功能。

###练习1.20:
> 在网站http://www.informit.com/store/c-plus-plus-primer-9780321714114 上，第1章的代码目录中包含了头文件Sales_item.h。将它拷贝到你自己的工作目录中。用它编写一个程序，读取一组书籍销售记录，将每条记录打印到标准输出上。

答:
```c++
#include<iostream>
#include"Sales_item.h"
int main()
{
 Sales_item book;
 std::cin >> book;
 std::cout << book << std::endl;
 return 0;
}
```

###练习1.21:
> 编写程序，读取两个ISBN相同的Sales_item对象，输出它们的和。

```c++
#include<iostream>
#include"Sales_item.h"
int main()
{
 Sales_item item1,item2;
 std::cin >> item1 >> item2;
 std::cout << item1 + item2 << std::endl;
 return 0;
}
```

###练习1.22:
> 编写程序，读取多个具有相同ISBN的销售记录，输出所有记录的和。

```c++
#include<iostream>
#include"Sales_item.h"
int main()
{
 Sales_item item_sum,item_val;
 while(std::cin >> item_val)
  item_sum += item_val;
 std::cout << item_sum << std::endl;
 return 0;
}
```

###练习1.23:
> 编写程序，读取多条销售记录，并统计每个ISBN(每本书)有几条销售记录。

```c++
#include<iostream>
#include"Sales_item.h"
int main()
{
 Sales_item item_curr,item_val;
 int cnt = 0;
 if(std::cin >> item_curr)
  {
   cnt += 1;
   while(std::cin >> item_val)
    {
     if(item_curr.isbn() == item_val.isbn())
      {
       ++cnt;
      }
     else
      {
       std::cout << item_curr.isbn() << " had " << cnt
                 << " records " << std::endl;
       item_curr = item_val;
       cnt = 1;
      }
    }
   std::cout << item_curr.isbn() << " had " << cnt
           << " records " << std::endl;
  }
 else
  std::cerr << "No data!" << std::endl;
 return 0;
}
```

###练习1.24:
> 输入表示多个ISBN的多条销售记录来测试上一个程序，每个ISBN的记录应该聚在一起。

答：输入多条测试即可。

###练习1.25:
> 借助网站上的Sales_item.h头文件，编译并运行本节给出的书店程序。

答：略。
