###练习5.1:
> 什么是空语句？什么时候会用到空语句？

答：最简单的语句是空语句，空语句中只含有一个单独的分号。如果在程序的某个地方，语法上需要一条语句但是逻辑上不需要，此时应该使用空语句。

###练习5.2:
> 什么是块？什么时候会用到块？

答：复合语句是指用花括号括起来的(可能为空的)语句和声明的序列，复合语句也被称为块。如果在程序的某个地方，语法上需要一条语句，但是逻辑上需要多条语句，则应该使用复合语句。

###练习5.3:
> 使用逗号运算符(参见4.10节，第140页)重写1.4.1节(第10页)的while循环，使它不再需要块，观察改写之后的代码的可读性提高了还是降低了。

答：
```c++
while(val <= 10)
 sum += val,++val;
```
很明显可读性降低了。

###练习5.4
> 说明下列例子的含义,如果存在问题,试着修改它.
```c++
(a)while (string::iterator iter != s.end()) { /*...*/ }
(b)while (bool status = find(word)) { /*...*/ }
    if(!status) { /*...*/ }
```

答:<br />
(a)iter应该在循环体外定义
```c++
string::iterator iter = s.begin()
while(iter != s.end()) { /*...*/ }
```

(b)status不在作用域内
```c++
bool status;
while(status = find(word)) { /*...*/ }
 if(!status) { /*...*/ }
```

###练习5.5:
> 写一段自己的程序,使用if else语句实现把数字成绩转换成字母成绩的要求.

答:<br />
```c++
 const vector<string> scores = {"F","D","C","B","A","A++"};
 unsigned grade;
 string lettergrade;
 if(grade < 60)
   lettergrade = scores[0];
  else
  {
   lettergrade = scores[(grade-50)/10];
   if(grade != 100) 
    if(grade % 10 > 7)
     lettergrade += '+'; 
    else if(grade % 10 < 3)
     lettergrade += '-';
```

###练习5.6:
> 改写上一题的程序,使用条件运算符(参见4.7节,第134页)代替if else语句.

答:<br />
```c++
(grade<60)?(lettergrade=scores[0]):(lettergrade=scores[(grade-50)/10]);
```

###练习5.7:
> 改正下列代码段中的错误.
```c++
(a)if(ival1 != ival2)
      ival1 = ival2
   else ival1 = ival2 = 0;
(b)if(ival < minval)
      minval = ival;
      occurs = 1;
(c)if(int ival = get_value())
    cout << "ival = " << ival << endl;
   if(!ival)
    cout << "ival = 0\n";
(d)if(ival = 0)
      ival = get_value();
```

答:<br />
(a)语法错误,缺少分号,修改为:ival1 = ival2;<br />
(b)应用花括号控制执行路径,修改为:
```c++
   if(ival < minval)
   {
    minval = ival;
    occurs = 1;
   }
```
(c)ival不在作用域内,应该在if语句之外定义ival,修改为:
```c++
   int ival;
   if(ival = get_value())
    cout << "ival = " << ival << endl;
   if(!ival)
    cout << "ival = 0\n";
```
(d)搞混了等号与赋值的区别,应修改为:
```c++
   if(ival == 0)
    ival = get_value();
```

###练习5.8:
> 什么是"悬垂else"?C++语言是如何处理else子句的?

答:当一个if语句嵌套在另一个if语句内部时,很可能if语句分支会多与else分支,这时候if else的匹配问题就称为"悬垂else",C++语言规定else与离它最近的尚未匹配的if匹配,从而消除了程序的二义性.

###练习5.9:
> 编写一段程序,使用一系列if语句统计从cin读入的文本中有多少元音字母.

答:<br />
```c++
#include<iostream>
using namespace std;
int main()
{
 unsigned aCnt = 0,eCnt = 0,iCnt = 0,oCnt = 0,uCnt = 0, vowelCnt = 0;
 char ch;
 while(cin >> ch)
  {
  switch(ch)
   {
    case 'a':
     ++aCnt;
     break;
    case 'e':
     ++eCnt;
     break;
    case 'i':
     ++iCnt;
     break;
    case 'o':
     ++oCnt;
     break;
    case 'u':
     ++uCnt;
     break;
    default:
     break;
   }
  }
 vowelCnt = aCnt + eCnt + iCnt + oCnt + uCnt;
 cout << vowelCnt << endl;
 return 0;
}
```

###练习5.10:
> 我们之前实现的统计元音字母的程序存在一个问题:如果元音字母以大写形式出现,不会被统计在内.编写一段程序,既统计元音字母的小写形式,也统计大写形式,也就是说,新程序遇到'a'和'A'都应该递增aCnt的值,以此类推.

答:以'a'为例,其他类似
```c++
case 'a':
case 'A':
 ++aCnt;
 break;
```

###练习5.11:
> 修改统计元音字母的程序,使其也能统计空格,制表符和换行符的数量.

答:定义相应的统计变量和case语句即可.
```c++
#include<iostream>
using namespace std;
int main()
{
 unsigned aCnt = 0,eCnt = 0,iCnt = 0,oCnt = 0,uCnt = 0,spaceCnt = 0,tabCnt = 0,newLineCnt = 0, vowelCnt = 0;
 char ch;
 while(cin >> noskipws >> ch)
  {
  switch(ch)
   {
    case 'a':
     ++aCnt;
     break;
    case 'e':
     ++eCnt;
     break;
    case 'i':
     ++iCnt;
     break;
    case 'o':
     ++oCnt;
     break;
    case 'u':
     ++uCnt;
     break;
    case '\t':
     ++tabCnt;
     break;
    case '\n':
     ++newLineCnt;
     break;
    case '\40':
     ++spaceCnt;
     break;
    default:
     break;
   }
  }
 vowelCnt = aCnt + eCnt + iCnt + oCnt + uCnt + spaceCnt + tabCnt + newLineCnt;
 cout << vowelCnt << endl;
 return 0;
}
```

###练习5.12:
> 修改统计元音字母的程序,使其能统计以下含有两个字符的字符序列的数量:ff,fl和fi.

答:<br />
```c++
#include<iostream>
using namespace std;
int main()
{
 unsigned ffCnt = 0,flCnt = 0,fiCnt = 0;
 char ch;
 bool f = false;
 while(cin >> ch)
  {
   if('f' == ch)
    f = true;
   if(f)
    {
     cin >>ch;
     switch(ch)
     {
      case 'f':
         ++ffCnt;
         break;
      case 'l':
         ++flCnt;
         break;
      case 'i':
         ++fiCnt;
         break;
      default:
         break;
     }
    }
  }
 cout << "ffCnt:\t" << ffCnt << endl;
 cout << "flCnt:\t" << flCnt << endl;
 cout << "fiCnt:\t" << fiCnt << endl;
 return 0;
}
```

###练习5.13:
> 下面显示的每个程序都含有一个常见的编程错误,指出错误在哪里,然后修改它们.
```c++
(a)unsigned aCnt = 0,eCnt = 0,iouCnt = 0;
   char ch = next_text();
   switch(ch){
    case 'a': aCnt++;
    case 'e': eCnt++;
    default:iouCnt++;
   }
(b)unsigned index = some_value();
   switch(index){
    case 1:
     int ix = get_value();
     ivec[ix] = index;
     break;
    default:
     ix = ivec.size()-1;
     ivec[ix]=index;
}
(c)unsigned evenCnt = 0,oddCnt = 0;
   int digit = get_num() % 10;
   switch(digit){
    case 1,3,5,7,9:
      oddcnt++;
      break;
    case 2,4,6,8,10:
      evencnt++;
      break;
   }
(d)unsigned ival = 512,jval = 1024,kval = 4096;
   unsigned bufsize;
   unsigned swt = get_bufCnt();
   switch(swt){
    case ival:
     bufsize = ival * sizeof(int);
     break;
    case jval:
     bufsize = jval * sizeof(int);
     break;
    case kval:
     bufsize = kval * sizeof(int);
     break;
   }
```

答:<br />
(a)缺少break语句.(只考虑语法的情况下)<br />
(b)c++语言规定不允许跨过变量的初始化语句直接跳转到该变量作用域内的另一位置.所以应该把ix的初始化语句放在switch语句之外.<br />
(c)不能省略case标签.另外oddCnt和evenCnt的书写错误.(此处应该不是作者的意图,而是印刷错误)<br />
(d)case标签必须是整型常量表达式,所以该程序段的第一句应该如下定义:
```c++
  const unsigned evenCnt = 0,oddCnt = 0;
```

###练习5.14:
> 编写一段程序,从标准输入中读取若干string对象并查找连续重复出现的单词.所谓连续重复出现的意思是:一个单词后面紧跟着这个单词本身.要求记录连续重复出现的最大次数以及对应的单词.如果这样的单词存在,输出重复出现的最大次数;如果不存在,输出一条信息说明任何单词都没有连续出现过.例如,如果是
```c++
how how now now now cow cow
```
那么输出应该表明单词now连续出现了3此.

答:<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
	vector<string> svec;
	string str;
	while(cin >> str)
		svec.push_back(str);
	vector<int> ivec;
	int cnt = 1;
	for(auto beg = svec.begin();beg != (svec.end() - 1);++beg)
		if(*beg == *(beg + 1))
			++cnt;
		else
		{
			ivec.push_back(cnt);
			cnt = 1;
		}
	ivec.push_back(cnt);
	string s = svec[0];
	int i = 0,x = 0;
	for(vector<int>::size_type ix = 0;ix != (ivec.size() - 1);++ix)
			if(ivec[ix] < ivec[ix + 1])
				i = (ix + 1);
	for(vector<int>::size_type ix = 0;ix != i;++ix)
		x += ivec[ix];
	cout << svec[x] << " " << ivec[i] << endl;
	return 0;
}
```

注:实现方法比较麻烦，改天再写个简单的。

###练习5.15:
> 说明下列循环的含义并改正其中的错误.
```c++
(a)for(int ix = 0;ix != sz;++ix){ /*...*/ }
   if(ix != sz)
	// ...
(b)int ix;
   for(ix != sz;++ix) { /*...*/ }
(c)for(int ix = 0;ix != sz;++ix,++ sz) { /*...*/ }
```

答:<br />
(a)ix不在作用域,应该把ix的定义放在for循环之外。<br />
(b)for循环的格式不对,应修改为for(int ix = 0;ix != sz;++ix)。<br />
(c)无休止的循环,应该把++sz删去。<br />

###练习5.16:
> while循环特别适用于那种条件保持不变,反复执行操作的情况,例如,当未达到文件末尾时不断读取下一个值.for循环则更像是在按步骤迭代,它的索引值在某个范围内依次变化.根据每种循环的习惯用法各自编写一段程序,然后分别用另一种循环改写.如果只能使用一种循环,你倾向于使用哪种呢?为什么?

答:<br />
```c++
vector<int> ivec;
int i;
while(cin >> i)
	ivec.push_back(i);

vector<int> ivec;
for(int i;cin >> i;)
	ivec.push_back(i);
```
更倾向于for吧,简单。

###练习5.17:
> 假设有两个包含整数的vector对象,编写一段程序,检验其中一个vector对象是否是另一个的前缀.为了实现这一目标,对于两个不等长的vector对象,只需挑出长度较短的那个,把它所有元素和另一个vector对象比较即可.例如,如果两个vector对象的元素分别是0,1,1,2和0,1,1,2,3,5,8,则程序的返回的结果应该为真.

答:<br />
```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
	vector<int> ivec1{ 0,1,1,2 },ivec2{ 0,1,1,2,3,5,8 };
	decltype(ivec1.size()) size = (ivec1.size()<ivec2.size()?ivec1.size():ivec2.size());
	bool status = true;
	for(decltype(ivec1.size()) ix = 0;ix != size;++ix)
	{
		if(ivec1[ix] != ivec2[ix])
		{
			status = false;
			break;
		}	
	}	
	if(status)
		cout << "Yes" << endl;
	else
		cout << "No" << endl;
	return 0;
}
```

###练习5.18:
> 说明下列循环的含义并改正其中的错误。
```c++
(a)do
	int v1,v2;
	cout << "Please enter two numbers to sum:";
	if(cin >> v1 >> v2)
		cout << "Sun is: " << v1 + v2 << endl;
   while(cin);
(b)do{
	   // ...
   } while(int ival = get_response);
(c)do{
	int ival = get_response();
} while(ival);
```

答：<br />
(a)缺少大括号。在do后面加上大括号。<br />
(b)不允许在条件部分定义变量。把变量的定义提到do while语句之前。<br />
(c)ival超出其作用域，把ival的定义提到do while语句之前。<br />

###练习5.19:
> 编写一段程序，使用do while循环重复地执行下述任务：首先提示用户输入两个string对象，然后挑出较短的那个并输出它。

答：<br />
```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
	string rsp;
	do
	{
		int val1,val2;
		cout << "Please enter two num:" << endl;
		cin >> val1 >> val2;
		cout << "The sum is: " << val1 + val2 << endl;
		cout << "More?(y or n):";
		cin >> rsp;
	}
	while(cin && rsp[0] != 'n');
	return 0;
}
```

###练习5.20:
> 编写一段程序，从标准输入中读取string对象的序列直到连续出现两个相同的单词或者所有单词都读完为止。使用while循环一次读取一个单词，当一个单词连续出现两次时用break语句终止循环。输出连续重复出现的单词，或者输出一个消息说明没有任何单词是连续重复出现的。

答：<br />
```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
	string str1,str2;
	bool fd = false;
	cout << "Please enter a serial of strings:" << endl;
	if(cin >> str1)
		while(cin >> str2)
		{
			if(str1 == str2)
			{
				cout << str2 << " have been found!" << endl;
				fd = true;
				break;
			}
			else
				str1 = str2;
		}	
	if(!fd)
		cout << "Not found!" << endl;
	return 0;
}
```

###练习5.21:
> 修改5.5.1节(第171页)练习题的程序，使其找到的重复单词必须以大写字母开头。

答：在上一题的第二个if判断中加上一个条件就可以了。
```c++
if(str1 == str2 && isupper(str2[0]))
```

###练习5.22:
> 本节的最后一个例子跳回到begin，其实使用循环能更好地完成该任务。重写这段代码，注意不再使用goto语句。

答：<br />
```c++
int sz = get_size();
while(sz <= 0)
{
	sz = get_size();
}
```

###练习5.23:
> 编写一段程序，从标准输入读取两个整数，输出第一个整数除以第二个整数的结果。

答：<br />
```c++
#include<iostream>
using namespace std;
int main()
{
	cout << "Please enter two nums:" << endl;
	int num1,num2;
	cin >> num1 >> num2;
	cout << "num1/num2:\t" << num1/num2 << endl;
	return 0;
}
```

###练习5.24:
> 修改你的程序，使得当第二个数是0时抛出异常。先不要设定catch子句，运行程序并真的为除数输入0,看看会发生什么？

答：<br />
```c++
#include<iostream>
#include<stdexcept>
using namespace std;
int main()
{
	cout << "Please enter two nums:" << endl;
	int num1,num2;
	while(cin >> num1 >> num2)
	try{
		if(num2 == 0)
		throw runtime_error("num2 is zero!");	
		cout << "num1/num2:\t" << num1/num2 << endl;
	}
	catch(runtime_error err)
	{
		
	}
	return 0;
}
```

当没有catch子句时编译不通过，提示:
```c++
main.cpp:18:9: error: expected ‘catch’ before numeric constant
```
当有catch子句时，其中若不包含任何代码，输入除数为0时，程序正常退出。<br />

注:若此处没有try、catch，仅有一条throw语句时程序可编译通过，当输入的第二个数是0时抛出异常。
```c++
terminate called after throwing an instance of 'std::runtime_error'
  what():  num2 is zero!
		   已放弃 (核心已转储)
```

###练习5.25:
> 修改上一题的程序，使用try语句块去捕获异常。catch子句应该为用户输出一条提示信息，询问其是否输入新数并重新执行try语句块的内容。

答：<br />
```c++
#include<iostream>
#include<stdexcept>
using namespace std;
int main()
{
	cout << "Please enter two num:" << endl;
	int num1,num2;
	while(cin >> num1 >> num2)
	try{
		if(num2 == 0)
		throw runtime_error("num2 is zero!");	
		cout << "num1/num2:\t" << num1/num2 << endl;
	}
	catch(runtime_error err)
	{
		cout << err.what()
			 << "\nTry again? Enter y or n" << endl;
		char c;
		cin >> c;
		if(!cin || c == 'n')
	    break;		
	}
	return 0;
}
```
