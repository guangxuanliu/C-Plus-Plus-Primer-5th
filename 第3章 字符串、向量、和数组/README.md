###练习3.1:
> 使用恰当的using声明重做1.4.1节(第11页)和2.6.2节(第67页)的练习。

答：把cin和cout替换一下就行。

###练习3.2:
> 编写一段程序从标准输入中一次读取一整行，然后修改该程序使其一次读入一个词。

答：
```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
 string line;
 while(getline(cin,line))
  cout << line << endl;
 //string word;
 //while(cin >> word)
 // cout << word << " ";
 //cout << endl;
 return 0;
}
```

###练习3.3:
> 请说明string类的输入运算符和getline函数分别是如何处理空白字符的。

答：<br />
string类的输入运算符：string对象会自动忽略开头的空白(即空格符、换行符、制表符等)，并从第一个真正的字符开始读起，直到遇见下一个空白为止。<br />
getline函数：从给定的输入流中读入内容，直到遇到换行符为止(注意换行符也被读进来了)，然后把所读的内容存到那个string对象中去(注意不存换行符)。getline只要一遇到换行符就结束读取操作并返回结果，哪怕输入的一开始就是换行符也是如此。如果输入真的一开始就是换行符，那么所得的结果是个空string。<br />

###练习3.4:
> 编写一个程序读入两个字符串，比较其是否相等并输出结果。如果不想等，输出较大的那个字符串。改写上述程序，比较输入的两个字符串是否等长，如果不等长，输出长度较大的那个字符串。

答：<br />
```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
 string str1,str2;
 cout << "Please enter two strings:" << endl;
 cin >> str1 >> str2;
 if(str1 == str2)
  cout << "str1 is equal to str2." << endl;
 else
  {
   cout << "the bigger one is：";
   if(str1 > str2)
    cout << str1 << endl;
   else
    cout << str2 << endl;
  }
/*
*  if(str1.size() == str2.size())
*   cout << "the two string has the same size." << endl;
*  else
*  {
*   cout << "the longer one is：";
*   if(str1.size() > str2.size())
*    cout << str1 << endl;
*   else
*    cout << str2 << endl;
*  }
*/
 return 0;
}
```

###练习3.5:
> 编写一段程序从标准输入中读入多个字符串并将它们连接在一起，输出连接成的大字符串。然后修改上述程序，用空格把输入的多个字符串分隔开来。

答：<br />
```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
 string str1, str2;
 while(cin >> str1)
//  str2 += str1;
  str2 += str1 + " ";
 cout << str2 << endl;
 return 0;
}
```

###练习3.6:
> 编写一段程序，使用范围for语句将字符串内得所有字符用X代替。

答：<br />
```c++
#include<iostream>
using namespace std;
int main()
{
 string str("some string");
 for(auto &c : str)
  if(!isspace(c))
   c = 'X';
 cout << str << endl;
 return 0;
}
```

###练习3.7:
> 就上一题完成得程序而言，如果将循环控制变量得类型设为char，将会发生什么？先估计一下结果，然后实际编程进行验证。

答：输出结果还是原字符串“some string”。

###练习3.8:
> 分别用while循环和传统得for循环重写第一题得程序，你觉得哪种形式更好呢？为什么？

答：
```c++
#include<iostream>
using namespace std;
int main()
{
 string str("some string");
 decltype(str.size()) index = 0;
 while(str[index])
  {
   if(!isspace(str[index]))
    str[index] = 'X';
   ++index;
  }
 cout << str << endl;
 return 0;
}
```
```c++
#include<iostream>
using namespace std;
int main()
{
 string str("some string");
 for(decltype(str.size()) index = 0;
     index < str.size();++index)
  if(!isspace(str[index]))
   str[index] = 'X';
 cout << str << endl;
 return 0;
}
```

范围for不用考虑字符串得范围，所以更简洁，使用起来更方便。

###练习3.9:
> 下面得程序有何作用？它合法吗？如何不合法，为什么？
```c++
string s;
cout << s[0] << endl;
```

答：不合法。s被默认初始化为空字符串，使用下标访问空string会引发不可预知的结果。但是C++标准并不要求标准库检测下标是否合法。在我的编译环境中输出空。

###练习3.10:
> 编写一段程序，读入一个包含标点符号的字符串，将标点符号去除后输出字符串剩余的部分。

答：
```c++
#include<iostream>
using namespace std;
int main()
{
 string str1,str2;
 cout << "Please enter a string:" << endl;
 while(getline(cin,str1))
  for(auto &c : str1)
  if(!ispunct(c))
   str2 += c;
 cout << str2 << endl;
 return 0;
}
```

###练习3.11:
> 下面的范围for语句合法吗？如果合法，c得类型是什么？
```c++
const string s = "Keep out!";
for(auto &c : s) { /*……*/ }
```

答：不合法，如果合法，则可以给c赋值从而改变string的值，但是string是const，所以是非法的。但是我的编译环境并没有报错，也没有给出警告。

###练习3.12:
> 下列vector对象的定义有不正确的吗？如果有，请指出来。对于正确的，描述其执行结果;对于不正确的，说明其错误原因。
```c++
(a)vector<vector<int>> ivec;<br />
(b)vector<string> svec = ivec;<br />
(c)vector<string> svec(10,"null");<br />
```

答：<br />
(a)正确，定义一个类型为vector<vector<int>>的变量。<br />
(b)错误，两个vector对象的类型不相同。<br />
(c)正确，svec有10个值为"null"的元素。<br />

###练习3.13:
> 下列的vector对象各包含多少个元素？这些元素的值分别是什么？
```c++
(a)vector<int> v1;<br />
(b)vector<int> v2(10);<br />
(c)vector<int> v3(10,42);<br />
(d)vector<int> v4{10};<br />
(e)vector<int> v5{10,42};<br />
(f)vector<string> v6{10};<br />
(g)vector<string> v7{10,"hi"};<br />
```

答：<br />
(a)0个元素。<br />
(b)10个元素，每个元素的值都为0。<br />
(c)10个元素，每个元素的值都为42。<br />
(d)1个元素，值为10.<br />
(e)2个元素，每个元素的值都为42.<br />
(f)10个元素，每个元素的值都为空。<br />
(g)10个元素，每个元素的值都为"hi"。<br />

###练习3.14:
> 编写一段程序，用cin读入一组整数并把它们存入一个vector对象。

答：<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
 vector<int> ivec;
 int num;
 while(cin >> num)
  ivec.push_back(num);
 return 0;
}
```

###练习3.15:
> 改写上题的程序，不过这次读入的是字符串。

答：<br />
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
 vector<string> svec;
 string str;
 while(cin >> str)
  svec.push_back(str);
 return 0;
}
```

###练习3.16:
> 编写程序，把练习3.13中vector对象的容量和具体内容输出出来。检查你之前的回答是否正确，如果不对，回头重新学习3.3.1节(第87页)直到弄明白错在何处为止。

答：
用v1举例，其他类似。
```c++
cout << v1.size() << endl;
for(auto i : v1)
 cout << i << endl;
```

###练习3.17:
> 从cin读入一组词并把它们存入一个vector对象，然后设法把所有词都该写为大写形式。输出改变后的结果，每个词占一行。

答：
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
 vector<string> svec;
 string str;
 while(cin >> str)
  svec.push_back(str);
 for(auto &st : svec)
 {
  for(auto &s : st)
   s = toupper(s);
  cout << st << endl;
 }
 return 0;
}
```

###练习3.18:
> 下面得程序合法吗？如果不合法，你准备如何修改？
```c++
vector<int> ivec;
ivec[0] = 42;
```

答：不合法。试图用下标访问一个不存在的元素，但是在编译时不会给出任何提示，在运行时会出现错误“段错误 (核心已转储)“。修改为：
```c++
vector<int> ivec;
ivec.push_back(42);
```

###练习3.19:
> 如果想定义一个含有10个元素的vector对象，所有元素的值都是42,请列举出三种不同的实现方法。哪种方法更好呢？为什么？

答：<br />
```c++
(a)vector<int> ivec = {42,42,42,42,42,42,42,42,42,42};
(b)vector<int> ivec(10,42);
(c)vector<int> ivec;
   for(int i = 1;i <= 10;++i)
    ivec.push_back(42);
```

对此题而言，第二种方法更好。

###练习3.20:
> 读入一组整数并把它们存入一个vector对象，将每对相邻整数的和输出出来。改写你的程序，这次要求先输出第1个和最后1个元素的和，接着输出第2个和倒数第2个元素的和，以此类推。

答：<br />
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
 vector<int> ivec;
 int num;
 while(cin >> num)
  ivec.push_back(num);
 if(ivec.size() % 2)
  {
   for(int i = 0;i < ivec.size()-2;i += 2)
    cout << ivec[i] + ivec[i+1] << endl;
   cout << ivec[ivec.size()-1] << endl;
  }
 else
  {
   for(int i = 0;i < ivec.size();i += 2)
   cout << ivec[i] + ivec[i+1] << endl;
  }
 return 0;
}
```
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
 vector<int> ivec;
 int num;
 while(cin >> num)
  ivec.push_back(num);
 if(ivec.size() % 2)
  {
   for(int i = 0;i < ivec.size()/2;++i)
    cout << ivec[i] + ivec[ivec.size()-1-i] << endl;
   cout << ivec[ivec.size()/2] << endl;
  }
 else
  {
   for(int i = 0;i < ivec.size();i += 2)
    cout << ivec[i] + ivec[ivec.size()-1-i] << endl;
  }
 return 0;
}
```

###练习3.21:
> 请使用迭代器重做3.3.3节(第94页)的第一个练习。

答：<br />
以v1为例，其它类似：<br />
```c++
for(auto it = v1.begin();it != v1.end();++it)
 cout << *it << endl;
```

###练习3.22:
> 修改之前那个输出text第一段的程序，首先把text的第一段全部改写成大写形式，然后再输出它。

答：
```c++
#include<iterator>
#include<string>
using namespace std;
int main()
{
 vector<string> svec;
 string str;
 while(cin >> str)
  svec.push_back(str);
 for(auto it = svec.begin();
     it != svec.end() && !it->empty();++it)
{
 if(it == svec.begin())
 {
  for(auto &c : *it)
   c = toupper(c);
  cout << *it << endl;
 }
 else
  cout << *it << endl;
}
 return 0;
}
```

###练习3.23:
> 编写一段程序，创建一个含有10个整数得vector对象，然后使用迭代器将所有元素的值都变成原来的两倍。输出vector对象的内容，检验程序是否正确。
```c++
#include<iostream>
#include<vector>
#include<iterator>
#include<string>
using namespace std;
int main()
{
 vector<int> ivec;
 for(int i = 1;i != 11;++i)
  ivec.push_back(i);
 for(auto it = ivec.begin();it != ivec.end();++it)
 {
  *it *= 2;
  cout << *it << endl;
 }
 return 0;
}
```

###练习3.24:
> 请使用迭代器重做3.3.3节(第94页)的最后一个练习。

答：<br />
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
 vector<int> ivec;
 int num;
 while(cin >> num)
  ivec.push_back(num);
 if(ivec.size() % 2)
  {
//   for(int i = 0;i < ivec.size()-2;i += 2)
//    cout << ivec[i] + ivec[i+1] << endl;
//   cout << ivec[ivec.size()-1] << endl;
   for(auto it = ivec.begin();it < ivec.end()-2; it += 2)
    cout << *it + *(it+1) << endl;
   cout << *(ivec.end()-1) << endl;
  }
 else
  {
//   for(int i = 0;i < ivec.size();i += 2)
//    cout << ivec[i] + ivec[i+1] << endl;
   for(auto it = ivec.begin();it < ivec.end();it += 2)
    cout << *it + *(it+1) << endl;
  }
 return 0;
}
```

###练习3.25:
> 3.3.3节(第93页)划分分数段的程序是使用下标运算符实现的，请利用迭代器改写程序并实现完全相同的功能。

答：<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
 vector<unsigned> scores(11,0);
 unsigned grade;
 auto it = scores.begin();
 while(cin >> grade)
  if(grade <= 100)
//   ++scores[grade/10];
   ++*(it+grade/10);
 for(auto i : scores)
  cout << i << " ";
 cout << endl;
 return 0;
}
```

###练习3.26:
> 在100页的二分搜索程序中，为什么用的是mid = beg + (end - beg)/2,而非mid = (beg + end)/2;？

答：因为迭代器无加法操作，见表3.7(第99页)。

###练习3.27:
> 假设txt_size是一个无参数的函数，它的返回值是int。请回答下列哪个定义是非法的？为什么？
```c++
unsigned buf_size = 1024;
(a)int ia[buf_size];	(b)int ia[4 * 7 - 14];
(c)int ia[txt_size()];	(d)char st[11] = "fundamental"
```

答：<br />
(a)非法，维度必须是一个常量表达式。但是我所在的编译环境中并没有报错。<br />
(b)合法。<br />
(c)非法，同(a)<br />
(d)非法，没有空间可存放空字符。<br />

###练习3.28:
> 下列数组中元素的值是什么？
```c++
string sa[10];
int ia[10];
int main()
{
 string sa2[10];
 int ia2[10];
}
```

答：<br />
sa中是10个空字符，<br />
ia中是10个0，<br />
sa2是10个空字符，<br />
ia2是未定义的值。

###练习3.29:
> 相比于vector来说，数组有哪些缺点，请列举一些。

答：大小固定，灵活性较差。不能随意向数组中添加元素。

###练习3.30:
> 指出下面代码中的索引错误。
 ```c++
constexpt size_t array_size = 10;
 int ia[array_size];
 for(size_t ix = 1;ix <= array_size;++ix)
  ia[ix] = ix;
```

答：数组的索引从0开始，该题目中的范围因该是大于等于0小于array_size。应修改为：
```c++
for(size_t ix = 0;ix < array_size;++ix)
```

###练习3.31:
> 编写一段程序，定义一个含有10个int的数组，令每个元素的值就是其下标值。
```c++
#include<iostream>
using namespace std;
int main()
{
 constexpr size_t array_size = 10;
 int ia[array_size];
 for(size_t ix = 0;ix < array_size;++ix)
  ia[ix] = ix;
 return 0;
}
```

###练习3.32:
> 将上一题刚刚创建的数组拷贝给另外一个数组。利用vector重写程序实现类似的功能。

答：<br />
```c++
#include<iostream>
using namespace std;
int main()
{
 constexpr size_t array_size = 10;
 int ia[array_size];
 for(size_t ix = 0;ix < array_size;++ix)
  ia[ix] = ix;
 int ia2[array_size];
 for(size_t ix = 0;ix <array_size;++ix)
  ia2[ix] = ia[ix];
 return 0;
}
```
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
 vector<int> ivec;
 for(int i = 0;i < 10;++i)
  ivec.push_back(i);
 vector<int> ivec2;
 for(auto it = ivec.begin();it != ivec.end();++it)
  ivec2.push_back(*it);
 return 0;
}
```

###练习3.33:
> 对于104页的程序来说，如果不初始化scores将发生什么？

答：输出的结果不正确。
    "和内置类型的变量一样，如果在函数内部定义了某种内置类型的数组，那么默认初始化会令数组含有未定义的值"(第101页)

###练习3.34:
> 假定p1和p2指向同一个数组中的元素，则下面程序的功能是什么？什么情况下该程序是非法的？
```c++
 p1 += p2 - p1;
```

答:此语句使得p1也指向p2原来所指向的元素。原则上说，只要p1和p2的类型相同，则该语句始终是合法的。只有当p1和p2不是同类型指针时，该语句才不合法（不能进行-操作）。 
<br />
但是，如果p1和p2不是指向同一个数组中的元素，则这个语句的执行结果可能是错误的。因为-操作的结果类型ptrdiff_t只能保证足以存放同一数组中两个指针之间的差距。如果p1和p2不是指向同一个数组中的元素，则-操作的结果有可能超出ptrdiff_t类型的表示范围而产生溢出，从而该语句的执行结果不能保证p1指向p2原来所指向的元素（甚至不能保证p1为有效指针）。 <br />
注：参考自CSDN(@sukyin)的答案：http://bbs.csdn.net/topics/240035816

###练习3.35:
> 编写一段程序，利用指针将数组中的元素置为0。
答：<br />
```c++
#include<iostream>
#include<iterator>
#include<vector>
using namespace std;
int main()
{
 constexpr size_t array_size = 10;
 int ia[array_size];
 for(size_t i = 0;i != array_size;++i)
  ia[i] = i;
 for(auto i : ia)
  cout << i << " ";
  cout <<  endl;
 int *beg = begin(ia);
 int *last = end(ia);
 for(;beg != last;++beg)
  *beg = 0;
 for(auto i : ia)
  cout << i << " ";
  cout << endl;
 return 0;
}
```

###练习3.36:
> 编写一段程序，比较两个数组是否相等。再写一段程序，比较两个vector对象是否相等。

答:<br />
```c++
#include<iostream>
#include<iterator>
#include<vector>
using namespace std;
int main()
{
 constexpr size_t array_size = 10;
 int ia1[array_size],ia2[array_size];
 for(size_t i = 0;i != array_size;++i)
 {
  ia1[i] = i;
  ia2[i] = 2*i;
 }
 int *beg_1 = begin(ia1),*end_1 = end(ia1);
 int *beg_2 = begin(ia2),*end_2 = end(ia2);
 bool eq = true;
 for(;beg_1 != end_1 || beg_2 != end_2;++beg_1,++beg_2)
  if(*beg_1 != *beg_2)
  {
   eq = false;
  }
 if(eq)
  cout << "the two arraies are equal!" << endl;
 else
  cout << "the two arraies are not equal!" << endl;
 return 0;
}
```
```c++
#include<iostream>
#include<iterator>
#include<vector>
using namespace std;
int main()
{
 vector<int> ivec1,ivec2;
 for(int i = 0;i != 10;++i)
 {
  ivec1.push_back(i);
  ivec2.push_back(2*i);
 }
 if(ivec1 == ivec2)
  cout << "the two containers are equal!" << endl;
 else
  cout << "the two containers are not equal!" << endl;
 return 0;
}
```

###练习3.37:
> 下面的程序是何含义，程序的输出结果是什么？
```c++
const char ca[] = {'h','e','l','l','o'};
const char *cp = ca;
while(*cp)
{
 cout << *cp << endl;
 ++cp;
}
```

答：程序循环输出ca[]中的内容"hello"之后输出了一串乱码。当程序输出最后一个字符的时候输出乱码，系统判定访问已越界，所以结束循环。我在while循环之前加上了一句代码ptrdiff_t n = end(ca) - begin(ca);之后程序只输出字符，没有输出乱码，应该是编译器的扩展(第102页)。

###练习3.38:
> 在本节中我们提到，将两个指针相加不但是非法的，而且也没有什么意义。请问为什么两个指针相加没有什么意义？

答：若两个指针相加，会将地址相加，而不是指针所指向的值。

###练习3.39:
> 编写一段程序，比较两个string对象，再编写一段程序，比较两个C风格字符串的内容。

答：<br />
```c++
#include<iostream>
#include<string>
#include<cstring>
using namespace std;
int main()
{
 string s1 = "A string example";
 string s2 = "A different string";
 if(s1 > s2)
  cout << "s1 > s2" << endl;
 const char ca1[] = "A string example";
 const char ca2[] = "A different string";
 if(strcmp(ca1,ca2) > 0)
  cout << "ca1 > ca2" << endl;
 return 0;
}
```

###练习3.40:
> 编写一段程序，定义两个字符数组并用字符串字面值初始化它们;接着再定义一个字符数组存放前两个数组连接后的结果。使用strcpy和strcat把前两个数组的内容拷贝到第三个数组中。

答：<br />
```c++
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
 const char ca1[] = "C++ Primer";
 const char ca2[] = "5th";
 constexpr size_t sz = strlen(ca1) + strlen(ca2) + 1;
 char largeStr[sz];
 strcpy(largeStr,ca1);
 strcat(largeStr," ");
 strcat(largeStr,ca2);
 const char *cp = largeStr;
 while(*cp)
 {
  cout << *cp;
  ++cp;
 }
 cout << endl;
 return 0;
}
```

###练习3.41:
> 编写一段程序，用整型数组初始化一个vector对象。

答：<br />
```c++
#include<iostream>
#include<vector>
#include<cstring>
using namespace std;
int main()
{
 constexpr size_t sz = 10;
 int arr[sz];
 for(int i = 0;i != sz;++i)
 {
  arr[i] = i;
 }
 //vector<int> ivec(begin(arr),end(arr));
 vector<int> ivec(arr,arr + sz);
 for(auto i : ivec)
  cout << i << endl;
 return 0;
}
```

###练习3.42:
> 编写一段程序，将含有整数元素的vector对象拷贝给一个整型数组。

答：<br />
```c++
#include<iostream>
#include<vector>
#include<cstring>
using namespace std;
int main()
{
 constexpr size_t sz = 10;
 int arr[sz];
 vector<int> ivec;
 for(int i = 0;i != sz;++i)
  ivec.push_back(i);
 for(auto i : ivec)
  cout << i << " ";
 cout << endl;
 for(int i = 0;i != sz;++i)
 {
  arr[i] = ivec[i];
 }
 for(auto i : arr)
  cout << i << " ";
 cout << endl;
 return 0;
}
```

###练习3.43:
> 编写3个不同版本的程序，令其均能输出ia的元素。版本1使用范围for语句管理迭代过程;版本2和版本3都使用普通的for语句，其中版本2要求用下标运算符，版本3要求用指针。此外，在所有3个版本的程序中都要直接写出数据类型，而不能使用类型别名、auto关键字或decltype关键字。

答：<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
 int ia[3][4] =
 {
  {0,1,2,3},
  {4,5,6,7},
  {8,9,10,11}
 };
//版本1,使用范围for语句管理迭代过程
 cout << "版本1,使用范围for语句管理迭代过程" << endl;
 for(int (&p)[4] : ia)
  for(int q : p)
  cout << q << " ";
 cout << endl;
//版本2,使用普通for语句，下标运算符
 cout << "版本2,使用普通for语句，下标运算符" << endl;
 for(size_t i = 0;i != 3;++i)
  for(size_t j = 0;j != 4;++j)
   cout << ia[i][j] << " ";
 cout << endl;
//版本3,使用普通for语句，指针
 cout << "版本3,使用普通for语句，指针" << endl;
 for(int (*p)[4] = ia;p != ia + 3;++p)
  for(int *q = *p;q != *p + 4;++ q)
   cout << *q << " ";
 cout << endl;
 return 0;
}
```

###练习3.44:
> 改写上一个练习中的程序，使用类型别名来代替循环控制变量的类型。

答：声明一下using int_array = int[4];然后把代码替换一下即可。

###练习3.45:
> 再一次改写程序，这次使用auto关键字。

答：<br />
把控制变量的类型替换为auto即可。


