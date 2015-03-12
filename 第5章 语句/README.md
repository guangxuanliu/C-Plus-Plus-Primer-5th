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
(a)语法错误,缺少分号,修改为:ival1 = ival2;
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
