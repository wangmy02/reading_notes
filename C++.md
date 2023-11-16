

# C++基础入门

## 1 C++初识

编写C++程序步骤

* 创建项目

* 创建文件

* 编写代码

* 运行程序

  

变量存在的意义：给一段指定的内存空间起名，方便操作内存

变量创建：数据类型 变量名=变量初始值；

常量作用：记录不可更改的数据，比如星期

方式：

* define宏常量  ： #define 常量名 常量值
* 关键字const 修饰变量也不可修改 ： const  数据类型 常量名=常量值

关键字作用：预先保留的单词（标识符），在定义变量或者常量时不要使用关键字



标识符命名规则：

* 标识符不能是关键字
* 标识符只能由字母、数字、下划线组成
* 第一个字符必须为字母或下划线
* 标识符中字母区别大小写

## 2 数据类型

数据类型存在意义：给变量分配合适的内存空间

### 2.1 整型

表示方式:   (所占内存空间不同)

* short   2字节    -32768~32767

* int        4字节    -2^31~2^31-1

* long     4字节 （Windows下）

* long long    8字节

  

总结：大小比较：short< int <= long <= long long

### 2.2 sizeof关键字

**作用**：统计数据类型所占内存大小

**语法**：sizeof(数据类型/变量)

### 2.3 实型（浮点型）

**作用**：表示小数

两类：（区别：表示的有效数字范围不同）

* 单精度float          **4字节**    7位有效数字
* 双精度double      **8字节**    15~16位有效数字

float f1=3.14；和float f1=3.14f; 

区别：第一种会将数据默认为双精度再转换为单精度

总结：

* 默认情况下，输出一个小数，会显示出6位有效数字d

科学计数法：

* float  f2=3e2;       ——3*10^2
* float  f3=3e-2;       ——3*0.1^2

### 2.4 字符型

**作用**：显示单个字符

**语法**： char ch='a';   

注：是单引号，里面一个字符

* 字符型变量占1个字节

* 字符型变量并不是把字符本身放到内存中存储，是放的对应ASCII编码

* 查看字符对应的ASCII码：

  cout<<(int)ch<<endl;          

  a——97 

  A——65

* 可直接用ASCII码给字符型变量赋值

   char ch='a'; 

  char  ch=97；

ASCII码由两部分组成：

- 非打印控制字符：0～31
- 打印字符：32～126　　键盘上能找到的

### 2.5 转义字符

**作用**：表示不能显示出来的字符

**掌握**：

* 换行符\n

* 反斜杠\ \          输出\

* 水平制表符\t        为了整齐输出数据    占八个空格

  `cout << "aaa\thelloworld" << endl;
   cout << "aa\thelloworld" << endl;
   cout << "aaaaa\thelloworld" << endl;`

### 2.6 字符串型

**作用：**表示一串字符

**两种风格**：

* C语言风格

  char str[] ="  ";

* C++风格  ——   包含头文件#include <string>

  string 变量名 = ” 字符串值“；

### 2.7 布尔类型 bool

* true ——真  ——输出1
* false ——假 ——输出0
* bool型变量占**1个字节**大小
* 输入非0的值都代表真

### 2.8 数据的输入

**作用**：从键盘获取数据

关键字：cin  >>

`bool flag =false;
 cin >> flag;         //输入
 cout << flag << endl;`

## 3 运算符

### 3.1 算术运算符

`+   -    + - * /  %  ++          ++            -- -- `

正号 负号                    取模（余）     ++a前置递增    a++后置递增

* 两个小数可以相除，结果可以是小数/整数
* 两个小数不可以做取模运算 ，只有整型变量可以做取模运算

### 3.2 赋值运算符

`= += -= *= /= %= `

### 3.3 比较（关系）运算符

`==     ！=      <     >     <=     >=`

### 3.4 逻辑运算符

**作用**：根据表达式的值返回真值或假值

* 与 &&

* 或 ||

* 非 ！

## 4 程序流程结构

* 顺序结构

* 选择结构

* 循环结构

  

### 4.1 选择结构

#### 4.1.1 if语句

单行 多行 多条件 嵌套

#### 4.1.2 三目运算符

表达式1？表达式2：表达式3

```C++
int a=10;
int b=20;
int c=0;

c=(a>b?a:b);     //将变量大的值赋给c
```

* 在C++中三目运算符返回的是变量，可以继续赋值

  `(a>b?a:b)=100;   //将100赋给变量大的值`

#### 4.1.3 switch语句

**作用**；执行多条件分支语句

**语法**：

```C++
switch(表达式)
{
   case 结果1: 执行语句;break;  
   
   case 结果2: 执行语句;break;
   …
   
   default： 执行语句;break;
}
```

* break：退出当前分支，不再向下执行，退出switch
* if和switch区别
  * switch缺点：判断时表达式只能是整型或者字符型，不可以是一个区间
  * 优点：结构清晰，执行率高

### 4.2 循环结构

#### 4.2.1 while循环

**案例描述：**系统随机生成一个1到100之间的数字，玩家进行猜测，如果猜错，提示玩家数字过大或过小，如果猜对恭喜玩家胜利，并且退出游戏。

```c++
#include <iostream>
using namespace std;
//time系统时间头文件包含

int main()
{
	//添加随机数种子 作用：利用当前系统时间生成随机数，防止每次随机数都一样
	srand((unsigned int)time(NULL));
	
	int num = rand() % 100 + 1;  //生成1~100的随机数
    
	int val = 0;
	while (1)
	{
		cin >> val;

		if (val > num)
		{
			cout << "猜测过大" << endl;

		}
		else if (val < num)
		{
			cout << "猜测过小" << endl;
		}
		else
		{
			cout << "你猜对了" << endl;
			break;   //跳出循环
		}
	}
	return 0;

}
```

#### 4.2.2 do while循环

**注意：**与while的区别在于do...while会 先执行一次循环语句，再判断循环条件

**练习案例：水仙花数**

**案例描述：**水仙花数是指一个 3 位数，它的每个位上的数字的 3次幂之和等于它本身

例如：1^3 + 5^3+ 3^3 = 153

请利用do...while语句，求出所有3位数中的水仙花数

```C++
#include <iostream>
using namespace std;

int main()
{
	int num = 100;
	do
	{
		int a = 0;  //个位
		int b = 0;  //十位
		int c = 0;  //百位

		a = num % 10;
		b = num / 10 % 10;
		c = num / 100;
		if (a*a*a+b*b*b+c*c*c==num)
		{
			cout << num << endl;
		}
		num++;
	} while (num < 1000);     //有分号
	return 0;
}
```

#### 4.2.3 for循环

* for循环结构比较清晰

  

**练习案例：敲桌子**

案例描述：从1开始数到数字100， 如果数字个位含有7，或者数字十位含有7，或者该数字是7的倍数，我们打印敲桌子，其余数字直接打印输出。

```c++
#include <iostream>
using namespace std;
int main()
{
	for (int i = 1; i <= 100; i++)
	{
		if ((i % 7 == 0) || (i % 10 == 7) || (i / 10 == 7))
		{
			cout << "敲桌子" << endl;
		}
		else
		{
			cout << i << endl;
		}	
	}
	return 0;
}
```

#### 4.2.4 嵌套循环

cout << endl;     //换行

cout <<j<<"*"<<i<<"=" << i * j<<"  ";

### 4.3 跳转语句

#### 4.3.1 break语句

**作用:** 用于跳出 选择结构 或者 循环结构

break使用的时机：

* 出现在switch条件语句中，作用是终止case并跳出switch
* 出现在循环语句中，作用是跳出当前的循环语句（跳出整个循环，不是当次循环）
* 出现在嵌套循环中，跳出最近的内层循环语句

#### 4.3.2 continue语句

**作用：**在**循环语句**中，跳过本次循环中余下尚未执行的语句，继续执行下一次循环

* continue并没有使整个循环终止，而break会跳出循环

#### 4.3.3 goto语句

**作用**：可以无条件跳转语句   （不推荐使用，程序流程容易混乱）

**语法：** `goto 标记;`

**解释：**如果标记的名称存在，执行到goto语句时，会跳转到标记的位置

```c++
#include <iostream>
using namespace std;
int main() {

	cout << "1" << endl;

	goto FLAG;

	cout << "2" << endl;
	cout << "3" << endl;
	cout << "4" << endl;

FLAG:

	cout << "5" << endl;
    system("pause");
    return 0;
}
```

## 5 数组

* 数组里的元素同一数据类型
* 放在一块连续的内存空间中

### 5.1 一维数组

一维数组定义的三种方式：

1. ` 数据类型  数组名[ 数组长度 ]; `
2. `数据类型  数组名[ 数组长度 ] = { 值1，值2 ...};`
3. `数据类型  数组名[ ] = { 值1，值2 ...};`

* 定义数组时必须有初始长度

#### 5.1.1 一维数组数组名

* 数组名（arr）是常量，代表首地址

一维数组名称的**用途**：

1. 可以统计整个数组在内存中的长度
   * sizeof(arr) ——整个数组长度
   * sizeof(arr[0]) ——某个元素占的大小
   * sizeof(arr) / sizeof(arr[0])  ——数组的元素个数
2. 可以获取数组在内存中的首地址

```C++
cout << "数组首地址为： " << (int)arr << endl;
	cout << "数组中第一个元素地址为： " << (int)&arr[0] << endl;
	cout << "数组中第二个元素地址为： " << (int)&arr[1] << endl;
```

* int将16进制转换为10进制

* &——取地址

  

**练习案例1**：五只小猪称体重

**案例描述：**

在一个数组中记录了五只小猪的体重，如：int arr[5] = {300,350,200,400,250};

找出并打印最重的小猪体重。

```c++
#include <iostream>
using namespace std;
int main()
{
	int arr[5] = { 300,350,200,400,250 };
	int max = 0;

	for (int i = 0; i < 5; i++)
	{
		if (arr[i] > max)
		{
			max = arr[i];
		}
		
	}
	cout << "最重的小猪体重为" << max << endl;
	return 0;
}
```

**方法**：找最大值——先认定最大值，再通过比较更新最大值



**练习案例2：**数组元素逆置

**案例描述：**请声明一个5个元素的数组，并且将元素逆置.

(如原数组元素为：1,3,2,5,4;逆置后输出结果为:4,5,2,3,1);

```C++
#include <iostream>
using namespace std;
int main()
{
	int arr[5] = { 1,3,2,5,4};
	int start = 0;
	int end = sizeof(arr) / sizeof(arr[0]) - 1;
	
	cout << "逆置前的数组为" << endl;
	for (int i = 0; i < 5; i++)
	{
		cout << arr[i] << "  ";
	}
	cout << endl;
	while (start<end)
	{
		int temp = arr[start];
		arr[start] = arr[end];
		arr[end] = temp;

		start++;
		end--;
	}
	
	cout << "逆置后的数组为" << endl;
	for (int i = 0; i < 5; i++)
	{
		cout << arr[i]<<"  ";
	}
    
	return 0;
}
```

**方法**：交换——创建空闲变量temp

#### 5.1.2 冒泡排序

**作用：** 最常用的排序算法，对数组内元素进行排序

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
2. 对每一对相邻元素做同样的工作，执行完毕后，找到第一个最大值。
3. 重复以上的步骤，每次比较次数-1，直到不需要比较

```c++
    for (int i = 0; i < 9 - 1; i++)
	{
		for (int j = 0; j < 9 - 1 - i; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
```

* 嵌套循环：排序轮数 每轮对比次数

### 5.2 二维数组

#### 5.2.1 二维数组定义方式

1. ` 数据类型  数组名[ 行数 ][ 列数 ]; `

2. `数据类型  数组名[ 行数 ][ 列数 ] = { {数据1，数据2 } ，{数据3，数据4 } };`        ——推荐

   ​        行

3. `数据类型  数组名[ 行数 ][ 列数 ] = { 数据1，数据2，数据3，数据4};`

4. ` 数据类型  数组名[  ][ 列数 ] = { 数据1，数据2，数据3，数据4};`

* 在定义二维数组时，如果初始化了数据，可以省略**行数**

#### 5.2.2二维数组数组名

int arr[2] [3]=
	{
		{1,2,3},
		{4,5,6}
	};

* 查看二维数组所占内存空间
  * 二维数组大小：sizeof(arr)
  * 二维数组一行大小： sizeof(arr[0]) 
  * 二维数组元素大小：sizeof(arr[0][0]) 
  * 二维数组行数： sizeof(arr) / sizeof(arr[0])
  * 二维数组列数： sizeof(arr[0]) / sizeof(arr[0][0]) 
* 获取二维数组首地址（ 加(int)把16进制转换为10进制 ）
  * 二维数组首地址： arr
  * 二维数组第一行地址： arr[0]
  * 二维数组第二行地址：arr[1]
  * 二维数组第一个元素地址：&arr[0] [0]
  * 二维数组第二个元素地址：&arr[0] [1]

#### **5.3.3 二维数组应用案例**

#### **5.3.3 二维数组应用案例**

**考试成绩统计：**

案例描述：有三名同学（张三，李四，王五），在一次考试中的成绩分别如下表，**请分别输出三名同学的总成绩**

|      | 语文 | 数学 | 英语 |
| ---- | ---- | ---- | ---- |
| 张三 | 100  | 100  | 100  |
| 李四 | 90   | 50   | 100  |
| 王五 | 60   | 70   | 80   |

```c++
#include <iostream>
using namespace std;
#include <string>
int main()
{
	int score[3][3]
	{
		{100,100,100},
		{90,50,100},
		{60,70,80}
	};

	string name[3] = { "张三","李四","王五" };
	for (int i = 0; i < 3; i++)
	{
		int sum = 0;
		for (int j = 0; j < 3; j++)
		{
			sum += score[i][j];
		}
		cout << name[i]<<"的总成绩是："<<sum << endl;
	}
	return 0;
}
```

## 6 函数

**作用：**将一段经常使用的代码封装起来，减少重复代码

函数的定义一般主要有5个步骤：

```c++
返回值类型 函数名 （参数列表） 
{
   函数体语句

   return表达式
}
```

```c++
int add(int num1, int num2)        //函数定义
{
	int sum = num1 + num2;
	return sum;
}
```



### 6.1 函数的调用

* 实参
* 形参
* 调用时，实参的值传给形参

### 6.2 值传递

* 所谓值传递，就是函数调用时实参将数值传入给形参

* **值传递时，如果形参发生改变，并不会影响实参**

  * main中两对输出结果相同

  ```c++
  void swap(int num1, int num2)
  {
  	int temp = num1;
  	num1 = num2;
  	num2 = temp;
  	
  	cout << "交换后：" << endl;
  	cout << "num1 = " << num1 << endl;
  	cout << "num2 = " << num2 << endl;
  }
  
  int main() {
  
  	int a = 10;
  	int b = 20;
  	
      cout << "a=" << a << endl;
      cout << "b=" << b << endl;
      
  	swap(a, b);
  	
  	cout << " a = " << a << endl;
  	cout << " b = " << b << endl;
  	
  	return 0;
  
  }
  ```

* 函数不需要返回值，声明函数时写void

### 6.3 函数的常见样式

常见的函数样式有4种

1. 无参无返
2. 有参无返
3. 无参有返
4. 有参有返

### 6.4 函数的声明

**作用**： 告诉编译器函数名称及如何调用函数。函数的实际主体可以单独定义。

*  函数的**声明可以多次**，但是函数的**定义**只能有一次

**声明**：

`int max(int a, int b);`

### 6.5 函数的分文件编写

**作用：**让代码结构更加清晰

函数分文件编写一般有4个步骤：

1. 创建后缀名为.h的头文件  
2. 创建后缀名为.cpp的源文件
3. **在头文件中写函数的声明**
4. **在源文件中写函数的定义**

**示例**：

```c++
//swap.h文件
#include<iostream>
using namespace std;

//实现两个数字交换的函数声明
void swap(int a, int b);

```

```c++
//swap.cpp文件
#include "swap.h"

void swap(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;

	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}
```

```c++
//main函数文件
#include "swap.h"
int main() {

	int a = 100;
	int b = 200;
	swap(a, b);

	system("pause");

	return 0;
}

```

## 7 指针

**指针的作用：** 可以通过指针间接访问内存

* 可以利用指针变量保存地址

### 7.1 指针变量的定义和使用

**语法**：`数据类型 * 变量名；`

```c++
int main() {
//1、指针的定义
int a = 10; //定义整型变量a

//指针定义语法： 数据类型 * 变量名 ;
int * p;

//指针变量赋值
p = &a; //指针指向变量a的地址
cout << &a << endl; //打印数据a的地址
cout << p << endl;  //打印指针变量p

//2、指针的使用
//通过*操作指针变量指向的内存
cout << "*p = " << *p << endl;

system("pause");

return 0;
}
```
* p存的a的地址
* *p指的a地址对应的值

**指针变量和普通变量的区别：**

* 普通变量存放的是数据,指针变量存放的是地址
* 指针变量可以通过" * "操作符，操作指针变量指向的内存空间，这个过程称为解引用



> 总结1： 我们可以通过 & 符号 获取变量的地址

> 总结2：利用指针可以记录地址

> 总结3：对指针变量解引用，可以操作指针指向的内存

### 7.2 指针所在内存空间

* 在**32**位操作系统下，指针是占**4**个字节空间大小，不管是什么数据类型（比如int *、float *）
* 在**64**位操作系统下，指针是占**8**个字节空间大小，不管是什么数据类型（比如int *、float *）

### 7.3 空指针和野指针

#### 7.3.1 空指针

**空指针**：指针变量指向内存中编号为0的空间

**用途：**初始化指针变量

```c++
//指针变量p指向内存地址编号为0的空间
	int * p = NULL;
```

**注意：**空指针指向的内存是不可以访问的    （0~255系统占用，不可访问）

访问：  *p=100;      ×

#### 7.3.2 野指针

**野指针**：指针变量指向非法的内存空间

```c++
	//指针变量p指向内存地址编号为0x1100的空间
	int * p = (int *)0x1100;
```

没有申请，例子中int a=10; 即是申请过程

**结论**：空指针和野指针都不是申请的空间，因此不要访问。

### 7.4 const修饰指针

const修饰指针有三种情况

1. const修饰指针   --- 常量指针   

   **const** int * p1 = &a;

   指针指向可以改，指针指向的值不可以更改

   ```c++
       int a = 10;
   	int b = 10;
   	
   	const int * p1 = &a; 
   	 p1 = &b;       //正确
   	//*p1 = 100;  报错
   ```

2. const修饰常量   --- 指针常量    

   int * **const** p2 = &a;

   指针指向不可以改，指针指向的值可以更改

   ```c++
       int * const p2 = &a;
   	//p2 = &b; //错误
   	*p2 = 100; //正确
   ```

3. const即修饰指针，又修饰常量

```c++
    const int * const p3 = &a;
	//p3 = &b; //错误
	//*p3 = 100; //错误
```

### 7.5 指针和数组

**作用：**利用指针访问数组中元素

* int * arr 也可以写为int arr[]

```c++
int main() {

	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };

	int * p = arr;  //指向数组的指针

	cout << "第一个元素： " << arr[0] << endl;
	cout << "指针访问第一个元素： " << *p << endl;

	for (int i = 0; i < 10; i++)
	{
		//利用指针遍历数组
		cout << *p << endl;
		p++;
	}

	system("pause");

	return 0;
}
```

### 7.6 指针和函数

**作用：**利用指针作函数参数，可以修改实参的值（与 值传递 的区别）

```c++
//值传递
void swap1(int a ,int b)
{
	int temp = a;
	a = b; 
	b = temp;
}
//地址传递
void swap2(int * p1, int *p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

int main() {

	int a = 10;
	int b = 20;
	swap1(a, b); // 值传递不会改变实参

	swap2(&a, &b); //地址传递会改变实参

	cout << "a = " << a << endl;

	cout << "b = " << b << endl;

	system("pause");

	return 0;
}
```

### 7.7 指针、数组、函数

**案例描述：**封装一个函数，利用冒泡排序，实现对整型数组的升序排序

例如数组：int arr[10] = { 4,3,6,9,1,2,10,8,7,5 };

```c++
//冒泡排序函数
void bubbleSort(int * arr, int len)  //int * arr 也可以写为int arr[]
{
	for (int i = 0; i < len - 1; i++)
	{
		for (int j = 0; j < len - 1 - i; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}

//打印数组函数
void printArray(int * arr, int len)
{
	for (int i = 0; i < len; i++)
	{
		cout << arr[i] << endl;
	}
}

int main() {

	int arr[10] = { 4,3,6,9,1,2,10,8,7,5 };
	int len = sizeof(arr) / sizeof(int);

	bubbleSort(arr, len);

	printArray(arr, len);

	system("pause");

	return 0;
}
```

* 当数组名传入到函数作为参数时，被退化为指向首元素的指针
* 对于数组作为函数参数的情况，我们有两种方式来声明函数：
  1. 使用指针方式：void printArray(int *arr, int len)
  2. 使用数组方式：void printArray(int arr[], int len)

## 8 结构体

结构体属于用户自定义数据类型，一些类型集合组成的一个类型

### 8.1 结构体定义和使用

**语法：**`struct 结构体名 { 结构体成员列表 }；`

```c++
//结构体定义
struct student
{
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
}stu3; //结构体变量创建方式3 
```

通过结构体创建变量的方式有三种：

* struct 结构体名 变量名

  ```c++
  struct student stu1; //struct 关键字可以省略
  
  	stu1.name = "张三";
  	stu1.age = 18;
  	stu1.score = 100;
  	
  	cout << "姓名：" << stu1.name << " 年龄：" << stu1.age  << " 分数：" << stu1.score << endl;
  ```

* struct 结构体名 变量名 = { 成员1值 ， 成员2值...}

  ```c++
  	struct student stu2 = { "李四",19,60 };
  ```

* 定义结构体时顺便创建变量

```c++
    stu3.name = "王五";
	stu3.age = 18;
	stu3.score = 80;
```

注：

* struct结构体变量通过“.”访问结构体中变量
* 定义结构体时的关键字是struct，不可省略
* 创建结构体变量时，关键字struct可以省略

### 8.2 结构体数组

**作用：**将自定义的结构体放入到数组中方便维护

**语法：**` struct  结构体名 数组名[元素个数] = {  {} , {} , ... {} }`

```c++
//结构体定义
struct student
{
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
}

int main() {
	
	//结构体数组
	struct student arr[3]=
	{
		{"张三",18,80 },
		{"李四",19,60 },
		{"王五",20,70 }
	};

	for (int i = 0; i < 3; i++)
	{
		cout << "姓名：" << arr[i].name 
		     << " 年龄：" << arr[i].age 
		     << " 分数：" << arr[i].score << endl;
	}

	system("pause");

	return 0;
}
```

创建结构体——创建结构体数组——赋值——遍历打印

### 8.3 结构体指针

**作用：**通过指针访问结构体中的成员

* 利用操作符 `-> `可以通过结构体指针访问结构体属性

```c++
//结构体定义
struct student
{
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};


int main() {
	
	struct student stu = { "张三",18,100, };
	
	struct student * p = &stu;
	
	p->score = 80; //指针通过 -> 操作符可以访问成员

	cout << "姓名：" << p->name << " 年龄：" << p->age << " 分数：" << p->score << endl;
	
	system("pause");

		return 0;
}
```

* 创建学生结构体变量
* 通过指针指向结构体变量
* 通过指针访问结构体变量中的数据

### 8.4 结构体嵌套结构体

**作用：**结构体中的成员可以是另一个结构体

**例如：**每个老师辅导一个学员，一个老师的结构体中，记录一个学生的结构体

* 定义学生结构体
* 定义老师结构体
* 创建老师

```c++
//学生结构体定义
struct student
{
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

//教师结构体定义
struct teacher
{
    //成员列表
	int id; //职工编号
	string name;  //教师姓名
	int age;   //教师年龄
	struct student stu; //子结构体 学生
};


int main() {

	struct teacher t1;
	t1.id = 10000;
	t1.name = "老王";
	t1.age = 40;

	t1.stu.name = "张三";
	t1.stu.age = 18;
	t1.stu.score = 100;

	cout << "教师 职工编号： " << t1.id << " 姓名： " << t1.name << " 年龄： " << t1.age << endl;
	
	cout << "辅导学员 姓名： " << t1.stu.name << " 年龄：" << t1.stu.age << " 考试分数： " << t1.stu.score << endl;

	system("pause");

	return 0;
}
```

### 8.5 结构体做函数参数

**作用：**将结构体作为参数向函数中传递

传递方式有两种：

* 值传递            

  `printStudent(s);`    

  `void printStudent(student s );`

* 地址传递

  `printStudent2(&s);`

  `void printStudent2(student *s);`

```c++
//学生结构体定义
struct student
{
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

//值传递
void printStudent(student stu )
{
	stu.age = 28;
	cout << "子函数中 姓名：" << stu.name << " 年龄： " << stu.age  << " 分数：" << stu.score << endl;
}

//地址传递
void printStudent2(student *stu)
{
	stu->age = 28;
	cout << "子函数中 姓名：" << stu->name << " 年龄： " << stu->age  << " 分数：" << stu->score << endl;
}

int main() {

	student stu = { "张三",18,100};
	//值传递
	printStudent(stu);
	cout << "主函数中 姓名：" << stu.name << " 年龄： " << stu.age << " 分数：" << stu.score << endl;

	cout << endl;

	//地址传递
	printStudent2(&stu);
	cout << "主函数中 姓名：" << stu.name << " 年龄： " << stu.age  << " 分数：" << stu.score << endl;

	system("pause");

	return 0;
}
```

### 8.6 结构体中const使用场景

地址传递优点：函数中的形参改为指针，可以减少内存空间，而且不会复制新的副本出来（节省空间）

```c++
void printStudent(const student *stu) //加const防止函数体中的误操作
{
	//stu->age = 100; //加入const之后，一旦有修改的操作就会报错，可以防止误操作
}
```

### 8.7 结构体案例

#### 8.7.1 案例1

**案例描述：**

学校正在做毕设项目，每名老师带领5个学生，总共有3名老师，需求如下

设计学生和老师的结构体，其中在老师的结构体中，有老师姓名和一个存放5名学生的数组作为成员

学生的成员有姓名、考试分数，创建数组存放3名老师，通过函数给每个老师及所带的学生赋值

最终打印出老师数据以及老师所带的学生数据。

```c++
#include <iostream>
using namespace std;
#include <ctime>
struct Student
{
	string sName;
	int score;
};
struct Teacher
{
	string tName;
	struct Student sArray[5];
};

//给老师和学生赋值
void allocateSpace(struct Teacher tArray[],int len)
{
	string nameSeed = "ABCDE";
	for (int i = 0; i < len; i++)
	{
		tArray[i].tName = "Teacher_";
		tArray[i].tName += nameSeed[i];

		for (int j = 0; j < 5; j++)
		{
			tArray[i].sArray[j].sName = "Student_";
			tArray[i].sArray[j].sName += nameSeed[i];
		

			int random = rand() % 61 + 40;
			tArray[i].sArray[j].score = random;
		}
	}
}
//打印所有信息
void printInfo(struct Teacher tArray[], int len)
{
	for (int i = 0; i < len; i++)
	{
		cout << "老师姓名：" << tArray[i].tName << endl;
		for (int j = 0; j < 5; j++)
		{
			cout << "\t学生姓名：" << tArray[i].sArray[j].sName 
				 << " 考试分数：" << tArray[i].sArray[j].score << endl;
		}
	}
}

int main()
{
	//随机数种子
	srand((unsigned int)time(NULL));
	Teacher tArray[3];
	
	int len = sizeof(tArray) / sizeof(tArray[0]);
	allocateSpace(tArray,len);
	printInfo(tArray, len);
	return 0;
}
```

注：可以使用数组的方式打印字符串，如下：

```C++ 
string name = "wang";
for (int i = 0; i < 4; i++)
	cout << name[i];
```

#### 8.7.2 案例2

**案例描述：**

设计一个英雄的结构体，包括成员姓名，年龄，性别;创建结构体数组，数组中存放5名英雄。

通过冒泡排序的算法，将数组中的英雄按照年龄进行升序排序，最终打印排序后的结果。

五名英雄信息如下：

```C++
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"},
```

```c++
#include <iostream>
using namespace std;
struct Hero
{
	string name;
	int age;
	string sex;
};
void bubbleSort(struct Hero hArray[], int len)
{
	for (int i = 0; i < len - 1; i++)
	{
		for (int j = 0; j < len - 1 - i; j++)
		{
			if (hArray[j].age > hArray[j + 1].age)
			{
				struct Hero temp = hArray[j];
				hArray[j] = hArray[j + 1];
				hArray[j + 1] = temp;
			}	
		}
	}
}
void printHero(struct Hero hArray[], int len)
{
	cout << "排序后：" << endl;
	for (int i = 0; i < len; i++)
	{
	
		cout <<"姓名：" <<hArray[i].name <<"  年龄：" <<hArray[i].age << "  性别："<<hArray[i].sex << endl;

	}
}
int main()
{
	struct Hero hArray[5] =
	{
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"}
	};
	int len = sizeof(hArray) / sizeof(hArray[0]);
	cout << "排序前：" << endl;
	for (int i = 0; i < len; i++)
	{
		cout << "姓名：" << hArray[i].name << "  年龄：" << hArray[i].age << "  性别：" << hArray[i].sex << endl;

	}

	bubbleSort(hArray, len);
	printHero(hArray, len);
	
	return 0;
}
```

* 结构体变量可直接交换，不用每个对应属性分别交换

# C++核心编程

## 1 内存分区模型

* 编译：将源代码通过编译器转换为可执行代码的过程。（代码——010101）
* 执行：将生成的可执行代码在计算机上运行的过程。

整个过程：先进行编译生成可执行文件，再将编译后的代码加载到内存中并由计算机执行的过程。



C++程序在执行时，将内存大方向划分为**4个区域**

- 代码区：存放函数体的二进制代码，由操作系统进行管理的

- 全局区：存放全局变量和静态变量以及常量

- 栈区：由编译器自动分配释放, 存放函数的参数值,局部变量等

- 堆区：由程序员分配和释放,若程序员不释放,程序结束时由操作系统回收

  

前两区执行前就有，后两区执行后才有



**内存四区意义：**

不同区域存放的数据，赋予不同的生命周期, 给我们更大的灵活编程

### 1.1 程序运行前

在程序编译后，生成了exe可执行程序，**未执行该程序前**分为两个区域：

**代码区：**

​		存放 CPU 执行的机器指令

​		代码区是**共享**的，共享的目的是对于频繁被执行的程序，只需要在内存中有一份代码即可

​		代码区是**只读**的，使其只读的原因是防止程序意外地修改了它的指令

**全局区：**

​		全局变量、静态变量、字符串常量、全局常量存放在此

​		局部变量，局部常量不在

​		（特点）该区域的数据**在程序结束后**由操作系统释放

总结：

* C++中在程序运行前分为全局区和代码区
* 代码区特点是共享和只读
* 全局区中存放全局变量、静态变量、常量
* 常量区中存放 const修饰的全局常量  和 字符串常量

### 1.2 程序运行后

​	**栈区：**

​		由编译器自动分配释放, 存放**函数的参数值**,**局部变量**等

​		注意事项：不要返回局部变量的地址，栈区开辟的数据由编译器自动释放

```c++
int * func()
{
	int a = 10;
	return &a;
}

int main() {

	int *p = func();

	cout << *p << endl;   //可以正确输出
	cout << *p << endl;   //栈区已释放

	system("pause");

	return 0;
}
```

   **堆区：**

​		由程序员分配释放,若程序员不释放,程序结束时由操作系统回收

​		在C++中主要利用new在堆区开辟内存（new关键字创建堆区数据）

**注意：**指针本质也是局部变量，放到栈上；指针存放的数据放到堆区

```c++
//要看
int* func()
{
    //指针本质也是局部变量，放到栈上；指针存放的数据放到堆区
	//栈区（a存的堆区地址） 堆区（初值为10）
    int* a = new int(10);
	return a;   //返回的初值为10的堆区数据地址
}

int main() {

	int *p = func();    //接收的初值为10的堆区数据地址（即堆区地址）

	cout << *p << endl;
	cout << *p << endl;
    
	system("pause");

	return 0;
}
```

### 1.3 new操作符

​    C++中利用**new操作符**在堆区开辟数据

​	堆区开辟的数据，由程序员手动开辟，手动释放，释放利用**操作符 delete**

​	语法：` new 数据类型`            

​               `new 数据类型[]`          ——开辟数组

​                `delete[] `                   ——释放数组

​    利用new创建的数据，会**返回该数据类型的指针**

```c++
int* func()
{
	//在堆区创建整型数据
	//new返回是 该数据类型的指针
	int* p = new int(10);
	return p;
}
void test01()
{
	int * p = func();
    cout << *p << endl;

	delete p;   //释放堆区数据

}
//在堆区开辟数组
void test02()
{
	//创建10个整型数据的数组，在堆区
	int * arr=new int[10];

	for (int i = 0; i < 10; i++)//赋值
	{
		arr[i] = i + 100;
	}
	for (int i = 0; i < 10; i++)
	{
		cout << arr[i] << endl;
	}
	//释放堆区数组
	delete[] arr;
}
int main()
{
	test01();
    test02();
	return 0;
}
```

* int * arr 也可以写成int arr[] 

## 2 引用

**作用：** 给变量起别名

**语法：** `数据类型 &别名 = 原名

```c++
    int a = 10;
	int &b = a;
```

* a、b指向同一块内存，所以修改b的值则a的值也改变

### 2.1 引用的注意事项

* 引用必须初始化

  ```c++
  int &b = a;  //正确
  int &b;      //错误
  ```

* 引用在初始化后，不可以改变

  （初始化是谁别名就是谁别名 不可以再作其他变量别名）

```c++
    int a = 10;
	int& b=a;
	int c = 20;   
	b = c;   //赋值操作，不是取别名操作，是给a、b变量代表的空间赋上新值c
```

### 2.2 引用做函数参数

**作用：**函数传参时，可以利用引用的技术让形参修饰实参（修改实参）

**优点：**可以简化指针修改实参

```c++
//1. 值传递
void swap01(int a, int b) {
	int temp = a;
	a = b;
	b = temp;
}

//2. 地址传递
void swap02(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

//3. 引用传递
void swap03(int& a, int& b) {
	int temp = a;
	a = b;
	b = temp;
}

//main函数中调用
swap01(a, b);
swap02(&a, &b);
swap03(a, b);
```

* 值传递  ——不能修饰实参
* 地址传递——能修饰实参
* 引用传递——能修饰实参（形参是实参的别名，所以操作的就是实参）
* 后两种达到的效果一样，但引用的语法更清楚简单

### 2.3 引用做函数返回值

作用：引用是可以作为函数的返回值存在的

注意：**不要返回局部变量引用**

​            函数调用可作为左值

```c++
//返回局部变量引用
int& test01() {
	int a = 10; //局部变量
	return a;
}

//返回静态变量引用
int& test02() {
	static int a = 20;
	return a;
}

int main() {

	//不能返回局部变量的引用
	int& ref = test01();
	cout << "ref = " << ref << endl;
	cout << "ref = " << ref << endl;

	//如果函数做左值，那么必须返回引用
	int& ref2 = test02();
	cout << "ref2 = " << ref2 << endl;
	cout << "ref2 = " << ref2 << endl;

	test02() = 1000;

	cout << "ref2 = " << ref2 << endl;
	cout << "ref2 = " << ref2 << endl;

	system("pause");

	return 0;
}
```

* 局部变量放在栈区，栈区上的数据在函数调用时分配，函数返回时释放。（即函数的执行期为生命周期）
* 静态变量放在全局区，全局区上的数据**在程序结束后**（即在程序的生命周期内一直存在）释放

### 2.4 引用的本质

**本质：**引用的本质在c++内部实现是一个**指针常量**

```c++
//可看
//发现是引用，转换为 int* const ref = &a;
void func(int& ref){
	ref = 100; // ref是引用，转换为*ref = 100
}
int main(){
	int a = 10;
    
    //自动转换为 int* const ref = &a; 指针常量是指针指向不可改，也说明为什么引用不可更改
	int& ref = a; 
	ref = 20; //内部发现ref是引用，自动帮我们转换为: *ref = 20;
    
	cout << "a:" << a << endl;
	cout << "ref:" << ref << endl;
    
	func(a);
	return 0;
}
```

### 2.5 常量引用

**作用：**常量引用主要用来修饰形参，防止**误操作**

在函数**形参列表**中，可以加**const**修饰形参，**防止形参改变实参**

```c++
//引用使用的场景，通常用来修饰形参
//加入const就可以了，编译器优化代码，int temp = 10; const int& ref = temp;
void showValue(const int& v) {
	//v += 10;
	cout << v << endl;
}

int main() {

	//函数中利用常量引用防止误操作修改实参
	int a = 10;
	showValue(a);

	system("pause");

	return 0;
}
```

## 3 函数提高

### 3.1 函数默认参数

在C++中，函数的形参列表中的形参是可以有默认值的。

语法：` 返回值类型  函数名 （参数= 默认值）{}`

* 如果在调用的时候传入了数据，就用自己的数据；没传入数据就用默认值。但是要保证参数列表的参数最后都有值
* 如果某个位置参数有默认值，那么从这个位置往后，从左向右，必须都要有默认值
* 如果函数声明有默认值，函数定义的时候就不能有默认参数

```C++
int func(int a, int b = 10, int c = 10) {
	return a + b + c;
}
int func2(int a = 10, int b = 10);
int func2(int a, int b) {
	return a + b;
}

int main() {

	cout << "ret = " << func(20, 20) << endl;
	cout << "ret = " << func(100) << endl;

	system("pause");

	return 0;
}
```

### 3.2 函数占位参数

C++中函数的形参列表里可以有占位参数，用来做占位，调用函数时必须填补该位置

**语法：** `返回值类型 函数名 (数据类型){}`

占位参数也可以有默认参数

```c++
//void func(int a, int =10) {}
void func(int a, int) {
	cout << "this is func" << endl;
}

int main() {

	func(10,10); //占位参数必须填补

	system("pause");

	return 0;
}
```

### 3.3 函数重载

#### 3.3.1 函数重载基本语法

**作用：**函数名可以相同，提高复用性

**函数重载满足条件：**

* 同一个作用域下（main外 现在写的函数都是全局函数——全局作用域）
* 函数名称相同
* 函数参数**类型不同**  或者 **个数不同** 或者 **顺序不同**

```c++
//函数重载
void func()
{
	cout << "func的调用" << endl;
}
void func(int a)
{
	cout << "func(int a)的调用" << endl;
}
void func(double a)
{
	cout << "func(double a)的调用" << endl;
}
void func(int a,double b)
{
	cout << "func(int a,double b)的调用" << endl;
}
void func(double a, int b)
{
	cout << "func(double a, int b)的调用" << endl;
}
int main()
{
	//func();
	//func(10);
	//func(3.14);
	//func(10, 3.14);
	func(3.14, 10);
	return 0;
}
```

**注意:**  函数的返回值不可以作为函数重载的条件

```c++
//×
int func(double a, int b)
{
	cout << "func(double a, int b)的调用" << endl;
	
}
```

#### 3.3.2 函数重载注意事项

* 引用作为重载条件
* 函数重载碰到函数默认参数（产生歧义，尽量避免写默认参数）

```c++
//要看
//1、引用作为重载条件
void func(int &a)
{
	cout << "func (int &a) 调用 " << endl;
}

void func(const int &a)
{
	cout << "func (const int &a) 调用 " << endl;
}

//2、函数重载碰到函数默认参数
void func2(int a, int b = 10)
{
	cout << "func2(int a, int b = 10) 调用" << endl;
}
void func2(int a)
{
	cout << "func2(int a) 调用" << endl;
}

int main() {
	
	int a = 10;
	func(a); //调用无const
	func(10);//调用有const  int &a=10;不合法 ；const int& a=10；合法

	//func2(10); //碰到默认参数产生歧义，不知道调用哪个，需要避免

	system("pause");

	return 0;
}
```

## 4 类和对象

C++面向对象的三大特性为：**封装、继承、多态**

C++认为万事万物都皆为对象，对象上有其属性和行为，人、车

具有**相同性质的**对象，我们可以抽象称为**类**，人属于人类，车属于车类

### 4.1 封装

#### 4.1.1 封装的意义

封装是C++面向对象三大特性之一

封装的意义：

* 将属性和行为作为一个整体，表现生活中的事物
* 将属性和行为加以权限控制

**封装意义1：**

**语法：** `class 类名{   访问权限： 属性  / 行为  };`

实例化：通过类名创建对象     `类名 对象名；`

 赋值：`对象名.属性；对象名.行为；`

**例1**

```c++
//圆周率
const double PI = 3.14;
//封装一个圆类，求圆的周长
//class代表设计一个类，后面跟着的是类名
class Circle
{
public:  //访问权限  公共的权限

	//属性
	int m_r;//半径

	//行为
	//获取到圆的周长
	double calculateZC()
	{
		//2 * pi  * r
		//获取圆的周长
		return  2 * PI * m_r;
	}
};
int main() {

	//通过圆类，创建圆的对象
	// c1就是一个具体的圆
	Circle c1;
	c1.m_r = 10; //给圆对象的半径 进行赋值操作

	cout << "圆的周长为： " << c1.calculateZC() << endl;

	system("pause");

	return 0;
}
```

**例2**

设计一个学生类，属性有姓名和学号，可以给姓名和学号赋值，可以显示学生的姓名和学号

```c++
class Student
{
public:
	string m_Name;
	int m_Id;
	void showStudent()
	{
		cout << "姓名：" << m_Name << "  学号：" << m_Id << endl;
	}
	void setName(string name)
	{
		m_Name = name;
	}
	void setId(int id)
	{
		m_Id = id;
	}
};
int main()
{
	Student s1;
	//s1.m_Name = "张三";
	//s1.m_Id = 1;
	s1.setName("张三");
	s1.setId(1);
	s1.showStudent();
	return 0;
}
```

注：类中的属性和行为统一称为成员

​        属性——成员属性

​        方法——成员函数 成员方法

**封装意义2：**

类在设计时，可以把属性和行为放在不同的权限下，加以控制

**访问权限**有三种：

1. public        公共权限        成员 类内可以访问，类外也可访问
2. protected 保护权限         成员 类内可以访问，类外不可访问，儿子可以访问父亲的保护内容
3. private      私有权限         成员 类内可以访问，类外不可访问，儿子不可以访问父亲的私有内容

后两种在继承时可以体现区别



```c++
class Person
{
public:
	string m_Name;
protected:
	string m_Car;
private:
	int m_Password;
public:
	void func()
	{
		m_Name = "张三";
	    m_Car = "拖拉机";
		m_Password = 123456;
	}
};
int main()
{
	Person p1;
	p1.m_Name = "李四";
	//p1.m_Car = "拖拉机"; //保护权限内容，类外访问不到
	//p1.m_Password = 123; //私有权限内容，类外访问不到
	return 0;
}
```

#### 4.1.2 struct和class的区别

在C++中 struct和class唯一的**区别**就在于 **默认的访问权限不同**

区别：

* struct 默认权限为公共
* class   默认权限为私有

```c++
class C1
{
	int  m_A; //默认是私有权限
};

struct C2
{
	int m_A;  //默认是公共权限
};

int main() {

	C1 c1;
	c1.m_A = 10; //错误，访问权限是私有

	C2 c2;
	c2.m_A = 10; //正确，访问权限是公共

	system("pause");

	return 0;
}
```

#### 4.1.3 成员属性设置为私有

**优点1：**将所有成员属性设置为私有，可以自己控制读写权限

* set_()    ——获取——只
* get_()   ——设置——写

**优点2：**对于写权限，我们可以检测数据的有效性

```c++
//要看
class Person {
public:

	//姓名设置可读可写
	void setName(string name) {
		m_Name = name;
	}
	string getName()
	{
		return m_Name;
	}

	//获取年龄 
	int getAge() {
		return m_Age;
	}
	//设置年龄
	void setAge(int age) {
		if (age < 0 || age > 150) {
			cout << "你个老妖精!" << endl;
			return;
		}
		m_Age = age;
	}

	//情人设置为只写
	void setLover(string lover) {
		m_Lover = lover;
	}
private:
	string m_Name; //可读可写  姓名
	int m_Age; //只读  年龄
	string m_Lover; //只写  情人
};
int main() {

	Person p;
	//姓名设置
	p.setName("张三");
	cout << "姓名： " << p.getName() << endl;

	//年龄设置
	p.setAge(50);
	cout << "年龄： " << p.getAge() << endl;

	//情人设置
	p.setLover("苍井"); //只写属性，不可以读取
	
    system("pause");
	return 0;
}
```



**练习案例1：设计立方体类**

设计立方体类(Cube)

求出立方体的面积和体积

分别用全局函数和成员函数判断两个立方体是否相等。

* 用全局函数判断两个对象时传入两个对象（参数）进行对比
* 用成员函数判断两个对象时用一个对象调用，传入另一个对象（参数）与自身进行比较

```c++
#include <iostream>
using namespace std;
class Cube
{
public:
	//设置获取长宽高
	//设置获取长
	void setL(int l)
	{
		m_L = l;
	}
	int getL()
	{
		return m_L;
	}
	//设置获取宽
	void setW(int w)
	{
		m_W = w;
	}
	int getW()
	{
		return m_W;
	}
	//设置获取高
	void setH(int h)
	{
		m_H = h;
	}
	int getH()
	{
		return m_H;
	}
	//获取面积
	int calculateS()
	{
		return 2 * m_L * m_H + 2 * m_H * m_W + 2 * m_W * m_L;
	}
	//获取体积
	int calculateV()
	{
		return m_L * m_H * m_W;
	}
	//利用成员函数判断两个立方体是否相等
	bool isSameByClass(Cube &c)
	{
		if (m_L == c.getL() && m_W == c.getW() && m_H == c.getH())
		{
			return true;
		}
		return false;
	}
private:
	int m_L;
	int m_H;
	int m_W;
};
//利用全局函数判断两个立方体是否相等
bool isSame(Cube &c1, Cube &c2)
{
	if (c1.getH() == c2.getH() && c1.getW() == c2.getW() && c1.getL() == c2.getL())
	{
		return true;
	}
	return false;
}
int main()
{
	Cube c1;
	c1.setL(10);
	c1.setH(10);
	c1.setW(10);

	cout << "c1的面积为：" << c1.calculateS() << endl;
	cout << "c1的体积为：" << c1.calculateV() << endl;

	Cube c2;
	c2.setL(10);
	c2.setH(10);
	c2.setW(10);

	bool ret = isSame(c1, c2);
	if (ret)
	{
		cout << "c1和c2是相等的" << endl;
	}
	else
	{
		cout << "c1和c2是不相等的" << endl;
	}
	ret = c1.isSameByClass(c2);
	if (ret)
	{
		cout << "c1和c2是相等的" << endl;
	}
	else
	{
		cout << "c1和c2是不相等的" << endl;
	}
	return 0;
}
```

**练习案例2：点和圆的关系**

设计一个圆形类（Circle），和一个点类（Point），计算点和圆的位置关系。（上、外、内）（在坐标系内）

**函数分文件编写**一般有4个步骤：

1. 创建后缀名为.h的头文件  
2. 创建后缀名为.cpp的源文件
3. **在头文件中写函数的声明**
4. **在源文件中写函数的定义**



**将类拆分出去实现分文件编写**

1. 创建后缀名为.h的头文件 

   创建类，并声明类（包括成员方法和成员属性）

2. 创建后缀名为.cpp的源文件

   对类的成员方法进行定义

   注意：**类名::方法名(){ }**

   ::  是作用域解析运算符，表明所属作用域，区分不同作用域同名函数

3. **在头文件中写函数的声明**

4. **在源文件中写函数的定义**



```c++
//point.h           ————————————实现成员函数声明和成员属性创建
#pragma once
#include <iostream>
using namespace std;
class Point
{
public:
	void setX(int x);

	int getX();

	void setY(int y);

	int getY();

private:
	int m_X;
	int m_Y;
};
```

```c++
//point.cpp               ——————————函数定义
#include "point.h"
void Point::setX(int x)
{
	m_X = x;
}
int Point::getX()
{
	return m_X;
}
void Point::setY(int y)
{
	m_Y = y;
}
int Point::getY()
{
	return m_Y;
}
```

```c++
//circle.h

#pragma once
#include <iostream>
using namespace std;
#include "point.h"

class Circle
{
public:
	void setR(int r);

	int getR();

	void setCenter(Point center);

	Point getCenter();

private:
	int m_R;
	Point m_Center;
};
```

```c++
//circle.cpp

#include "circle.h"

void Circle::setR(int r)
{
	m_R = r;
}
int Circle::getR()
{
	return m_R;
}
void Circle::setCenter(Point center)
{
	m_Center = center;
}
Point Circle::getCenter()
{
	return m_Center;
}

```

```c++
#include <iostream>
using namespace std;
#include "circle.h"
#include "point.h"

//判断点和圆的关系
void isInCircle(Circle &c,Point &p)
{
	int distance=
	(c.getCenter().getX() - p.getX())* (c.getCenter().getX() - p.getX()) +
	(c.getCenter().getY() - p.getY()) * (c.getCenter().getY() - p.getY());
	int rDistance= c.getR() * c.getR();

	if (distance == rDistance)
	{
		cout << "点在圆上" << endl;
	}
	else if (distance > rDistance)
	{
		cout << "点在圆外" << endl;
	}
	else
	{
		cout << "点在圆内" << endl;
	}
}
int main()
{
	Circle c;
	c.setR(10);
	Point center;
	center.setX(10);
	center.setY(10);
	c.setCenter(center);

	Point p;
	p.setX(10);
	p.setY(10);

	isInCircle(c, p);
	return 0;
}
```

* 注意头文件的包含

### 4.2 对象的初始化和清理

#### 4.2.1 构造函数和析构函数

对象的初始化和清理分别由**构造函数**和**析构函数**实现

* 构造函数：主要作用在于**创建对象**时为对象的成员属性**赋值**，构造函数由编译器**自动调用**，无须手动调用。
* 析构函数：主要作用在于**对象销毁前**系统**自动调用**，执行一些**清理**工作。

注：如果我们不提供构造和析构，编译器会提供，但是编译器提供的构造函数和析构函数是空实现

**构造函数语法：**`类名(){}`

1. 构造函数，没有返回值也不写void
2. 函数名称与类名相同
3. **构造函数可以有参数，因此可以发生重载**
4. 程序在调用对象时候会自动调用构造，无须手动调用,而且只会调用一次

**析构函数语法：** `~类名(){}`

1. 析构函数，没有返回值也不写void
2. 函数名称与类名相同,在名称前加上符号  ~
3. **析构函数不可以有参数，因此不可以发生重载**
4. 程序在对象销毁前会自动调用析构，无须手动调用,而且只会调用一次

```c++
class Person
{
public:
	//构造函数
	Person()
	{
		cout << "Person构造函数的调用" << endl;
	}
	//析构函数
	~Person()
	{
		cout << "Person析构函数的调用" << endl;
	}
};
void test01()
{
	Person p; //在栈上的数据，test01执行完毕后就释放这个对象，所以执行完test01即完成了对象p的构造和析构
}


int main()
{
	test01();
	system("pause");
	return 0;
}
```

#### 4.2.2 构造函数的分类及调用

**两种分类方式：**

- ​	按参数分为： 有参构造和无参（默认）构造

```c++
Person()    
	{
		cout << "Person的无参（默认）构造函数调用" << endl;
	}
	Person(int a)
	{
		age = a;
		cout << "Person的有参构造函数调用" << endl;
	}
```

- ​	按类型分为： 普通构造和拷贝构造

```c++
	//拷贝构造函数
	Person(const Person &p)
	{
		age = p.age;//将传入的人身上所有属性，拷贝到自己身上
		cout << "Person的拷贝构造函数调用" << endl;

	}
```

**三种调用方式：**(擅长一种)

- ​    括号法

```c++
void test01()
{
    Person p;         //默认构造函数调用
    Person p2(10);    //有参构造函数
    Person p3(p2);    //拷贝构造函数  
}
```

​	注意：调用默认构造函数时候，不要加（）

​                eg:  `Person p1();`   编译器会认为是函数的声明，不会认为在创建对象

-  显示法

```c++
 void test01
 {
    Person p1;
	Person p2 = Person(10);
	Person p3 = Person(p2);
 }
```

注意：`Person(10); `是匿名对象 

​            特点：当前行执行结束，系统会立即回收掉匿名对象

- ​	隐式转换法

```c++
void test01()
{
	Person p2 = 10;//相当于 Person（10）；有参构造
	Person p3 = p2; //拷贝构造
}
```

注意：隐式转换法可以和显示对应记

#### 4.2.3 拷贝构造函数调用时机

C++中拷贝构造函数调用时机通常有三种情况

* 使用一个已经创建完毕的对象来初始化一个新对象

  ```c++
  void test01()
  {
      Person p1(20);      //有参构造
      Person p2(p1);      //拷贝构造
  }
  ```

* **值传递**的方式给函数参数传值       (传对象——给对象开辟新空间)

  值传递——拷贝一块新空间

  ```c++
  void doWork(Person p)  //值传递——拷贝一块新空间——拷贝构造对象
  {
  
  }
  void test02()
  {
       Person p;     //有参构造
       doWork(p);    //值传递
  }
  ```

  

* 以值方式返回局部对象

```c++
Person doWork2()
{
    Person p1;    //有参构造 因是局部变量，函数执行完变量即销毁，因此拷贝一份给return;
    return p1;    //拷贝构造
}
void test03()
{
    Person p=doWork2();
}
```

#### 4.2.4 构造函数调用规则

默认情况下，c++编译器至少给一个类添加3个函数

1．默认构造函数(无参，函数体为空)

2．默认析构函数(无参，函数体为空)

3．默认拷贝构造函数，对属性进行值拷贝



构造函数**调用规则**如下：

* 如果用户定义有参构造函数，c++不在提供默认无参构造，但是会提供默认拷贝构造


* 如果用户定义拷贝构造函数，c++不会再提供其他构造函数

```c++
class Person {
public:
	//无参（默认）构造函数
	Person() {
		cout << "无参构造函数!" << endl;
	}
	//有参构造函数
	Person(int a) {
		age = a;
		cout << "有参构造函数!" << endl;
	}
	//拷贝构造函数
	Person(const Person& p) {
		age = p.age;
		cout << "拷贝构造函数!" << endl;
	}
	//析构函数
	~Person() {
		cout << "析构函数!" << endl;
	}
public:
	int age;
};

void test01()
{
	Person p1(18);
	//如果不写拷贝构造，编译器会自动添加拷贝构造，并且做浅拷贝操作
	Person p2(p1);

	cout << "p2的年龄为： " << p2.age << endl;
}

void test02()
{
	//如果用户提供有参构造，编译器不会提供默认构造，会提供拷贝构造
	Person p1; //此时如果用户自己没有提供默认构造，会出错
	Person p2(10); //用户提供的有参
	Person p3(p2); //此时如果用户没有提供拷贝构造，编译器会提供

	//如果用户提供拷贝构造，编译器不会提供其他构造函数
	Person p4; //此时如果用户自己没有提供默认构造，会出错
	Person p5(10); //此时如果用户自己没有提供有参，会出错
	Person p6(p5); //用户自己提供拷贝构造
}

int main() {

	test01();

	system("pause");
	return 0;
}
```

#### 4.2.5 深拷贝和浅拷贝

浅拷贝：简单的赋值拷贝操作（编译器提供的那种）

深拷贝：在堆区重新申请空间，进行拷贝操作



浅拷贝带来的问题是堆区的内存重复释放，深拷贝用来解决浅拷贝的问题



注意：指针是局部变量，放在栈区；但是指针存放的数据放在堆区

​            并注意new的用法

```c++
class Person {
public:
	Person()       
    {
		cout << "无参构造函数!" << endl;
	}
	Person(int age ,int height) {
		
		cout << "有参构造函数!" << endl;
		m_age = age;
		m_height = new int(height);
	}
	Person(const Person& p) {
		cout << "拷贝构造函数!" << endl;
		m_age = p.m_age;
        //m_height=p.m_height;  //编译器默认实现这行代码，
		m_height = new int(*p.m_height);
	}
	//析构函数
	~Person() {
		cout << "析构函数!" << endl;
		if (m_height != NULL)
		{
			delete m_height;
		}
	}
public:
	int m_age;
	int* m_height;
};

void test01()
{
	Person p1(18, 180);

	Person p2(p1);

	cout << "p1的年龄： " << p1.m_age << " 身高： " << *p1.m_height << endl;

	cout << "p2的年龄： " << p2.m_age << " 身高： " << *p2.m_height << endl;
}

int main() {

	test01();
    
	system("pause");
	return 0;
}
```

**结论：**如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题（如指针保存的数据）

#### 4.2.6 初始化列表

**作用：**  **初始化列表**用来初始化属性

**语法：**`构造函数()：属性1(值1),属性2（值2）... {}`

```c++
//要看
Person(int a, int b, int c)
{
	m_A = a;
	m_B = b;
	m_C = c;
}

Person(10,20,30);

//等同于
    
Person():m_A(10),m_B(20),m_C(30)
{

}

//等同于

Person(int a,int b,int c): m_A(a),m_B(b),m_C(c)  
{
    
}

Person(10,20,30);    
```

#### 4.2.7 类对象作为类成员

C++类中的成员可以是另一个类的对象，我们称该成员为 对象成员

```c++
class A {}
class B
{
    A a；
}
```

B类中有对象A作为成员，A为**对象成员**



**结论：**

* 构造顺序：当其他类对象作为本类成员，构造时先构造类对象，再构造自身

​     （即上述 先构造A对象，再构造B对象）

- 析构顺序：与构造顺序相反

  （即上述 先析构B对象，再析构A对象）

```c++
class Phone
{
public:
	Phone(string name)
	{
		m_PhoneName = name;
		cout << "Phone构造" << endl;
	}

	~Phone()
	{
		cout << "Phone析构" << endl;
	}

	string m_PhoneName;
};

class Person
{
public:

	Person(string name, string pName) :m_Name(name), m_Phone(pName)
	{
		cout << "Person构造" << endl;
	}

	~Person()
	{
		cout << "Person析构" << endl;
	}

	void playGame()
	{
		cout << m_Name << " 使用" << m_Phone.m_PhoneName << " 牌手机! " << endl;
	}

	string m_Name;
	Phone m_Phone;

};
void test01()
{

	Person p("张三" , "苹果X");
	p.playGame();

}

int main() {

	test01();
	system("pause");
	return 0;
}
```

#### 4.2.8 静态成员

静态成员就是在成员变量和成员函数前加上关键字**static**，称为静态成员

静态成员分为：

*  静态成员变量
   *  所有对象共享同一份数据
   *  在编译阶段分配内存  （全局区）
   *  类内声明，类外初始化  （一定要初始化）
*  静态成员函数
   *  所有对象共享同一个函数
   *  静态成员函数只能访问静态成员变量



**静态成员变量**

* 静态成员变量，不属于某个对象上，所有对象都共享一份数据。因此静态成员变量有两种访问方式

  * 通过对象进行访问

    ```c++
    类名 对象名；  //创建对象
    cout<<对象名.静态变量名<<endl；  //访问
    ```

  * 通过类名进行访问

    ```c++
    cout<<类名::静态变量名<<endl;
    ```

* 静态成员变量也有访问权限，类外访问不到私有的静态成员变量

```c++
//可看
class Person
{
public:
	static int m_A;
	//静态成员变量也有访问权限
private:
    static int m_B;
};
int Person::m_A = 100;
int Person::m_B = 200;
void test01()
{
	Person p;
	cout << p.m_A << endl;

	Person p2;
	p.m_A = 200;
	cout << p.m_A << endl;
}
void test02()         //访问
{
	//通过对象进行访问
	//Person p;
	//cout << p.m_A << endl;
	//通过类名进行访问
	cout << Person::m_A << endl;

	//cout << Person::m_B << endl; 类外访问不到私有的静态成员变量
}
int main()
{
	//test01();
	test02();
	return 0;
}
```

**静态成员函数**

* 两种访问方式：

  * 通过对象进行访问
  * 通过类名进行访问

* 静态成员函数 不可以访问 非静态成员变量，无法区分到底是哪个对象的成员属性

  **解释：**

  如下程序创建对象

  ```
  Person p1;
  p1.func();
  
  Person p2;
  p2.func();
  ```

  如果访问`int m_B;`的m_B，则不知道是p1的m_B还是p2的m_B，

  但如果访问`static int m_A;`的m_A，则不管是哪个对象 访问的是同一个m_A

  

```c++
//可看
class Person
{

public:

	static void func()
	{
		cout << "func调用" << endl;
		m_A = 100;
		//m_B = 100; //错误，不可以访问非静态成员变量
	}
	static int m_A; //静态成员变量
	int m_B; // 
private:

	//静态成员函数也是有访问权限的
	static void func2()
	{
		cout << "func2调用" << endl;
	}
};
int Person::m_A = 10;

void test01()
{
	//静态成员变量两种访问方式

	//1、通过对象
	Person p1;
	p1.func();

	//2、通过类名
	Person::func();

	//Person::func2(); //私有权限访问不到
}

int main() {

	test01();

	system("pause");
	return 0;
}
```

### 4.3 对象模型和this指针

#### 4.3.1 成员变量和成员函数分开存储

* 类内的成员变量和成员函数分开存储
* 只有非静态成员变量才属于类的对象上

（静态成员变量、非静态成员函数、静态成员函数均不属于类对象上，因只有一份，类对象共同使用）

* 每个空对象也应该有一个独一无二的内存地址，为了区分空对象占内存的位置，编译器会给每个空对象也分配一个字节空间

  因此空对象占用的内存空间为1

* 当对象不为空时，对象占用的内存空间即为其所有成员（非静态成员变量）的大小

```c++
class Person
{
    int m_A;          //属于类的对象上
    
    static int m_B;   //不属于
    
    void func(){}     //不属于
    
    static void func2(){}  //不属于
}
int Person::m_B=0;
void test01()
{
    Person p;
    cout<<p.size()<<endl;
}
int main()
{
    test01();
    return 0;
}
```

#### 4.3.2 this指针概念

* 通过this指针，解决多个同类型对象调用同一个非静态成员函数，如何区分哪个对象调用自己的的问题

* this指针**指向被调用的成员函数所属的对象**
* this指针是隐含每一个非静态成员函数内的一种指针

this指针的用途：

* 当形参和成员变量同名时，可用this指针来区分

  ```c++
  class Person
  {
  public:
      Person(int age)
      {
        this->age=age;
      }
      
      int age;
  };
  
  Person p;   //this指向p
  ```

* 在类的非静态成员函数中返回**对象本身**，可使用return *this

注意：一个类的成员函数返回值类型是类名&，这意味着该函数返回的是**对当前对象的引用**，而不是一个新的对象。在需要返回对象本身的情况下会使用。

```c++
class Person
{
public:
    Person& PersonAddPerson(Person &p)
    {
    this->age +=p.age;
    
    return *this;
    }
};
void test 01()
{
    Person p1(10);
    Person p2(10);
   
    //链式编程思想
  p2.PersonAddPerson(p1).PersonAddPerson(p1).PersonAddPerson(p1); 
    cout << "p2.age = " << p2.age << endl;    //输出40
}
```

#### 4.3.3 空指针访问成员函数

空指针可以调用成员函数，但要

```c++
	Person * p = NULL;
	cout << this->m_Age << endl;  //此时应先判断指针是否为空，如果为空，程序崩溃
```



```c++
//要看
class Person {
public:

	void ShowClassName() {
		cout << "我是Person类!" << endl;
	}
	
	void ShowPerson() {
		if (this == NULL) {
			return;
		}
		cout << this->m_Age << endl;
	}

public:
	int m_Age;
};

void test01()
{
	Person * p = NULL;
	p->ShowClassName(); //空指针，可以调用成员函数
	p->ShowPerson();  //但是如果成员函数中用到了this指针，就不可以了
}

int main() {

	test01();

	system("pause");
	return 0;
}
```

#### 4.3.4 const修饰成员函数

**常函数：**

* 成员函数后（函数体）加const后我们称为这个函数为**常函数**
* 常函数内不可以修改成员属性
* 成员属性声明时加关键字mutable后，在常函数中依然可以修改

**注：**

* this指针的本质是一个指针常量，指针的指向不可修改

  即`Person * const this;`

* 在成员函数后面加const，修饰的是this指针，让指针指向的值也不可以修改

  即 `const Person * const this;`

  

**常对象：**

* 声明对象前加const称该对象为常对象

  `const Person p;  //常对象` 

* 常对象只能调用常函数

  解释：常对象的成员属性不可以修改，但是普通成员函数可以修改属性，如果常对象调用了普通成员函数则修改了自己的成员属性，所以常对象只能调用常函数

**注：**

* 常对象的成员属性不能被修改
* 在常函数和常对象下给成员属性加关键字mutable都可以被修改

```c++
//要看
class Person
{
     public:
     void showPerson()const
     {
        this->m_A=1000;  //报错，因为this指向的值不可以修改
        （扩：this = NULL: //this指针不可以修改指针的指向）
    
        this->m_B=1000; //正确，因为m_B声明时加了mutable关键字
    }
    
    void func()
    {
        m_A=1000;  //
    }
     
     public:
     int m_A;
     mutable int m_B;  //特殊变量，即使在常函数中，也可以修改这个值
}
void test01()
{
     const Person p; //常对象
     p.m_A=100;   //报错，常对象的成员属性也不能被修改
     p.m_B=100;   //正确
    
    //常对象只能调用常函数
    p.showPerson();  //正确
    p.func();        //报错,常对象的成员属性m_A不可以修改，但是func()函数里修改了m_A的值，矛盾
}
```

### 4.4 友元

**目的：**让一个 函数或者类 访问另一个类中 私有成员

友元的关键字：**friend**

友元的三种实现

* 全局函数做友元
* 类做友元
* 成员函数做友元

#### 4.4.1 全局函数做友元

全局函数访问类私有成员

用法：将全局函数在类内声明，并在前面加 friend 关键字（写到类里就行，无关访问权限）

```c++
class Building
{
	//告诉编译器 goodGay全局函数 是 Building类的好朋友，可以访问类中的私有内容
	friend void goodGay(Building * building);

public:

	Building()
	{
		this->m_SittingRoom = "客厅";
		this->m_BedRoom = "卧室";
	}

public:
	string m_SittingRoom; //客厅

private:
	string m_BedRoom; //卧室
};


void goodGay(Building * building)
{
	cout << "好基友全局函数正在访问： " << building->m_SittingRoom << endl;
	cout << "好基友全局函数正在访问： " << building->m_BedRoom << endl;
}

void test01()
{
	Building b;
	goodGay(&b);
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

#### 4.4.2 类做友元

类访问类私有成员

* A访问B类中的私有成员

  ```c++
  class B
  {
     friend class A;
  }
  ```

* 动态创建对象： `对象名=new 类名；`，new返回一个指向该对象的指针

  `Person* person = new Person;`

* 类内声明，类外实现类成员函数

  `类名::函数名（）{}`

```c++
class Building;
class goodGay
{
public:

	goodGay();
	void visit();

private:
	Building *building;
};


class Building
{
	//告诉编译器 goodGay类是Building类的好朋友，可以访问到Building类中私有内容
	friend class goodGay;

public:
	Building();

public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom;//卧室
};

Building::Building()
{
	this->m_SittingRoom = "客厅";
	this->m_BedRoom = "卧室";
}

goodGay::goodGay()
{
	building = new Building;
}

void goodGay::visit()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void test01()
{
	goodGay gg;
	gg.visit();

}

int main(){

	test01();

	system("pause");
	return 0;
}
```

#### 4.4.3 成员函数做友元

成员函数访问（另一个类）的私有成员

* A访问B类中的私有成员

  ```c++
  class B
  {
     friend 返回类型 类名::A  A成员函数名 ();
  }
  ```

  

```c++
class Building;
class goodGay
{
public:

	goodGay();
	void visit(); //只让visit函数作为Building的好朋友，可以发访问Building中私有内容
	void visit2(); 

private:
	Building *building;
};


class Building
{
	//告诉编译器  goodGay类中的visit成员函数 是Building好朋友，可以访问私有内容
	friend void goodGay::visit();

public:
	Building();

public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom;//卧室
};

Building::Building()
{
	this->m_SittingRoom = "客厅";
	this->m_BedRoom = "卧室";
}

goodGay::goodGay()
{
	building = new Building;
}

void goodGay::visit()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void goodGay::visit2()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	//cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void test01()
{
	goodGay  gg;
	gg.visit();

}

int main(){
    
	test01();

	system("pause");
	return 0;
}
```

**注：**上述 类做友元 和 成员函数做友元 的区别在于 只是在另一个类中声明谁做友元的问题

### 4.5 运算符重载

**概念：**对已有的运算符重新进行定义，赋予其另一种功能，以适应不同的数据类型

#### 4.5.1 加号运算符重载

作用：实现两个自定义数据类型相加的运算

​            对于内置数据类型，编译器知道如何进行计算（比如int+int、float+float、double+double）

```c++
class Person
{
   public:
      int m_A;
      int m_B;
}

Person p1;
p1.m_A=10;
p1.m_B=10;

Person p2;
p2.m_A=10;
p2.m_B=10;
```

* 成员函数实现运算符重载

  ```c++
  Person operator+ (Person &p)
  {
     Person temp;
     temp.m_A=this->m_A+p.m_A;
     temp.m_B=this->m_B+p.m_B;
  }
  
  Person p3=p1.operator+ (p2);  //成员函数重载本质调用
  简化为
  Person p3=p1+p2;
  ```

  

* 全局函数实现运算符重载

```C++
Person operator+ (Person& p1, Person& p2)
{
    Person temp;
    temp.m_A = p1.m_A + p2.m_A;
	temp.m_B = p1.m_B + p2.m_B;
	return temp;
}

Person p3=operator+ (p1,p2);   //全局函数重载本质调用
简化为
Person p3=p1+p2;
```

* 运算符重载可以发生函数重载

```C++
Person operator+(Person& p2, int num)  
{
	Person temp;
	temp.m_A = p2.m_A + num;
	temp.m_B = p2.m_B + num;
	return temp;
}

Person p3=p1+10;
```

注意：

* 对于内置的数据类型的表达式的的运算符是不可能改变的

* 不要滥用运算符重载（比如重载加法 函数内却实现减法）



#### 4.5.2 左移运算符重载

作用：可以输出自定义数据类型

​            想直接输出对象（类类型）（通过输出对象从而输出属性）

* 无法利用成员函数重载<<运算符，因为无法实现cout在左侧

* 只能利用全局函数重载<<运算符

  

```C++
//ostream对象只能有一个
ostream & operator<<(ostream &cout,Person &p)
{
    cout<<"m_A="<<p.m_A<<" m_B="<<p.m_B;
    return cout;  //否则下述endl报错，因为没有返回cout对象
}

Person p1;
p1.m_A=10;
p1.m_B=10;
cout<<p<<endl;     //本质： operator<<(cout, p)
```

注：重载左移运算符配合友元可以实现输出自定义数据类型

​        因为通常类成员属性设为私有

#### 4.5.3 递增运算符重载

作用： 通过重载递增运算符，实现自己的整型数据

* 重载前置++运算符 

  * 要返回引用，以便一直对一个数据进行递增操作

  * 先进行++运算，//再将自身做返回

    ```c++
     MyInteger& operator++()
        {
            m_Num++;
            return *this；
        }
    ```

* 重载后置++运算符

  * 参数要用int代表占位，可以自动区分前置和后置，只认int

  * 先记录当时结果，后递增，最后将记录结果做返回

    ```c++
        MyInteger operator++(int)      
        {
            MyInteger temp=*this;
            m_Num++;
            return temp;
        }
    ```

    

```C++
//要看
//自定义整型
class MyInteger
{
   friend ostream& operator<<(ostream &cout,MyInteger &myint);
   public:
    MyInteger()
    {
        n_Num=0;
    }
   
    
    //重载前置++运算符  返回引用为了一直对一个数据进行递增操作
    MyInteger& operator++()
    {
        //先进行++运算
        m_Num++;
        //再将自身做返回
        return *this；
    }
    
    //重载后置++运算符
    MyInteger operator++(int)        //int代表占位，可以区分前置和后置，只认int
    {
        //先 记录当时结果
        MyInteger temp=*this;
        //后 递增
        m_Num++;
        //最后将记录结果做返回
        return temp;
    }
    private:
        int m_Num;
};
ostream& operator<<(ostream &cout,MyInteger &myint)
{
    cout<<myint.m_Num;
    return cout;
}  

void test01()
{
    MyInteger myint;
    cout<<++(++myint)<<endl;
    cout<<myint<<endl;
}
void test02()
{
    MyInteger myint;
    cout<<myint++<<endl;
    cout<<myint<<endl;
}
int main()
{
    test01();
    test02();
}
```

#### 4.5.4 赋值运算符重载

c++编译器至少给一个类添加4个函数

1. 默认构造函数(无参，函数体为空)
2. 默认析构函数(无参，函数体为空)
3. 默认拷贝构造函数，对属性进行值拷贝
4. 赋值运算符 operator=, 对属性进行值拷贝

如果类中有属性指向堆区，做**赋值操作**时也会出现深浅拷贝问题(重复释放同一块内存)

```c++
//可看
class Person
{
public:

	Person(int age)
	{
		//将年龄数据开辟到堆区
		m_Age = new int(age);
	}

	//重载赋值运算符 
	Person& operator=(Person &p)
	{
        //先判断是否有属性在堆区，如果有，先释放干净，然后再深拷贝
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
		//编译器提供的代码是浅拷贝
		//m_Age = p.m_Age;

		//提供深拷贝 解决浅拷贝的问题
		m_Age = new int(*p.m_Age);

		//返回自身
		return *this;
	}


	~Person()
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
	}

	//年龄的指针
	int *m_Age;

};


void test01()
{
	Person p1(18);
	Person p2(20);
	Person p3(30);

	p3 = p2 = p1; //赋值操作

	cout << "p1的年龄为：" << *p1.m_Age << endl;
	cout << "p2的年龄为：" << *p2.m_Age << endl;
	cout << "p3的年龄为：" << *p3.m_Age << endl;
}

int main() {

	test01();

	system("pause");
	return 0;
}
```

 C++ 通过赋值运算符解决浅拷贝的问题和通过拷贝函数实现浅拷贝的问题 两种方式的区别

* 赋值运算符用于将一个对象的值复制到另一个对象
* 拷贝构造函数用于创建一个新对象，并将另一个对象的值复制到新对象。

#### 4.5.6 关系运算符重载

**作用：**重载关系运算符，可以让两个自定义类型对象进行对比操作

比如：直接比较两个类对象

```c++
class Person
{
    public:
      Person(string name,int age)
      {
          this->m_Name=name;
          this->age=age;
      }
    
    //关系运算符重载 ==
     bool operator== (Person &p)
     {
         if(this->m_Name==p.m_Name&&this->m_Age==p.m_Age)
         {
             return true;
         }
         else
         {
             return false;
         }
     }
    
      //关系运算符重载 !=
      bool operator!= (Person &p)
     {
         if(this->m_Name==p.m_Name&&this->m_Age==p.m_Age)
         {
             return false;
         }
         else
         {
             return true;
         }
     }
    
    
    string m_Name;
    int m_Age;
}
void test01()
{
    Person p1("Tom",18);  
    Person p2("Tom",18);
    
    if (p1 == p2)
	{
		cout << "p1和p2相等" << endl;
	}
	else
	{
		cout << "p1和p2不相等" << endl;
	}

	if (p1 != p2)
	{
		cout << "p1和p2不相等" << endl;
	}
	else
	{
		cout << "p1和p2相等" << endl;
	}
}
int main()
{
    test01();
    
    return 0;
}
```

#### 4.5.7 函数调用运算符重载

* 函数调用运算符 ()  也可以重载
* 由于重载后使用的方式非常像函数的调用，因此称为**仿函数**
* 仿函数没有固定写法，非常灵活



```c++
//打印输出类
class MyPrint
{
public:
	void operator()(string test)
	{
		cout << test << endl;
	}

};
void MyPrint02(string test)
{
    cout << test << endl;
}
void test01()
{
	//重载的（）操作符 也称为仿函数
	MyPrint myPrint;
	myPrint("hello world");   //使用起来类似于函数调用，所以叫仿函数
    MyPrint02("hello world");
}

//加法类
class MyAdd
{
public:
	int operator()(int v1, int v2)
	{
		return v1 + v2;
	}
};

void test02()
{
	MyAdd myadd;
	int ret =myadd(100, 100);
	cout << "ret = " << ret << endl;

	//匿名函数对象调用  类型（）    （不用创建对象）
	cout << "MyAdd()(100,100) = " << MyAdd()(100, 100) << endl;
}

int main() {

	test01();
	test02();

	system("pause");

	return 0;
}
```

### 4.6 继承

#### 4.6.1 继承的基本语法

好处：减少重复的代码

语法：`class 子类: 继承方式 父类 `

* 子类 又称 派生类
* 父类 又称 基类

派生类中的成员，包含**两大部分**：

一类是从基类继承过来的，一类是自己增加的成员。

从基类继承过过来的表现其共性，而新增的成员体现了其个性。

#### 4.6.2 继承方式

**继承方式一共有三种：**

* 公共继承
* 保护继承
* 私有继承

![](F:\大四学习\C++\image\微信图片_20231114155645.png)

**总结：**

1. public继承：基类中的public属性和protected属性在派生类中可访问且属性权限均不变，基类中的private属性不可访问。
2. protected继承：基类中的public属性和protected属性在派生类中可访问且均变成protected属性，基类中的private属性不可访问。
3. private继承：基类中的public属性和protected属性在派生类中可访问且均变成private属性，基类中的private属性不可访问

#### 4.6.3 继承中的对象模型

* 父类中所有非静态成员属性都会被子类继承
* 父类中私有成员属性被子类继承下去了，但是被编译器隐藏所以访问不到

利用开发人员命令提示工具查看对象模型

* 跳转盘符 ：     G： 
* 跳转文件路径： cd G:\C++\C++核心编程\C++核心编程
* 查看命名 ：      cl  /d1   reportSingleClassLayout  类名 所属文件名

#### 4.6.4 继承中构造和析构的顺序

继承中 创建子类对象 先调用父类构造函数，再调用子类构造函数，析构顺序与构造相反

#### 4.6.5 继承同名成员处理方式

当子类与父类出现同名的成员(成员属性、成员函数)，通过子类对象访问子类或父类中同名的数据 方法：

* 访问子类同名成员   直接访问即可      `s.m_A`
* 访问父类同名成员   需要加作用域      `s.Base::m_A`



```c++
class Base
{
    Base()
    {
       m_A=100;
    }
    void func()
    {
        cout<<"Base-func()调用"<<endl;
    }
    void func(int a)
	{
		cout << "Base - func(int a)调用" << endl;
	}
    int m_A;
};
class Son:public Base
{
    Son()
    {
       m_A=200;
    }
    void func()
    {
        cout<<"Son-func()调用"<<endl;
    }
    int m_A;
};
//同名成员属性处理
void test01()
{
     Son s;
     cout<<"Son下m_A="<<s.m_A<<endl;  //输出200
     cout<<"Base下m_A="<<s.Base::m_A<<endl;  //输出100
}
//同名成员函数处理
void test02()
{
    Son s;
    s.func();         //调用子类同名成员函数
    s.Base::func();   //调用父类同名成员函数
    
    s.func(10);       //报错
    s.Base::func(10); //正确输出
}
```

**注意：**当子类与父类拥有同名的成员函数，子类会隐藏父类中同名成员函数（包括重载函数，只要函数名一样），加作用域可以访问到父类中同名函数

#### 4.6.6 继承同名静态成员处理方式

处理子类和父类同名静态成员的方式和上述非静态成员一致：

- 访问子类同名成员   直接访问即可

  （两种访问方式：通过对象 和 通过类名）

- 访问父类同名成员   需要加作用域

  （两种访问方式：通过对象 和 通过类名）

```c++
class Base {
public:
	static void func()
	{
		cout << "Base - static void func()" << endl;
	}
	static void func(int a)
	{
		cout << "Base - static void func(int a)" << endl;
	}

	static int m_A;
};

int Base::m_A = 100;

class Son : public Base {
public:
	static void func()
	{
		cout << "Son - static void func()" << endl;
	}
	static int m_A;
};

int Son::m_A = 200;

//同名成员属性
void test01()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	cout << "Son  下 m_A = " << s.m_A << endl;   //200
	cout << "Base 下 m_A = " << s.Base::m_A << endl;//100

	//通过类名访问
	cout << "通过类名访问： " << endl;
	cout << "Son  下 m_A = " << Son::m_A << endl;
    //第一个::代表通过类名访问  第二个代表Base作用域下
	cout << "Base 下 m_A = " << Son::Base::m_A << endl;
}

//同名成员函数
void test02()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	s.func();
	s.Base::func();

	cout << "通过类名访问： " << endl;
	Son::func();
	Son::Base::func();
	//出现同名，子类会隐藏掉父类中所有同名成员函数，需要加作作用域访问
	Son::Base::func(100);
}
int main() {

	//test01();
	test02();

	system("pause");

	return 0;
}
```

#### 4.6.7 多继承语法

C++允许**一个类继承多个类**

语法：` class 子类 ：继承方式 父类1 ， 继承方式 父类2...`

多继承可能会引发父类中有同名成员出现，需要加作用域区分（所以实际开发中不采用）

```c++
class Base1 {
public:
	Base1()
	{
		m_A = 100;
	}
public:
	int m_A;
};

class Base2 {
public:
	Base2()
	{
		m_A = 200;  //改为mA就会出现不明确
	}
public:
	int m_A;
};
class Son : public Base2, public Base1 
{
public:
	Son()
	{
		m_C = 300;
		m_D = 400;
	}
public:
	int m_C;
	int m_D;
};
void test01()
{
	Son s;
	cout << "sizeof Son = " << sizeof(s) << endl;  //16
	cout << s.Base1::m_A << endl;          //100
	cout << s.Base2::m_A << endl;          //200
}
```

#### 4.6.8 菱形继承

* **菱形继承概念：**

​	两个派生类继承同一个基类

​	又有某个类同时继承者两个派生类

​	这种继承被称为菱形继承，或者钻石继承

* 菱形继承的主要问题：子类继承两份相同的数据，导致资源浪费以及毫无意义

* 利用**虚继承**可以解决菱形继承问题

​        语法：继承前加**virtual**关键字后，变为虚继承，而基类被称为虚基类

​        `class B : virtual public A {};`

​        实质：两个子类分别继承指针，通过各自偏移量找到唯一的数据（基类）



菱形继承问题：

1.     羊继承了动物的数据，驼同样继承了动物的数据，当草泥马使用数据时，就会产生二义性。
2.     草泥马继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以。

```c++
//要看
class Animal
{
public:
	int m_Age;
};
//继承前加virtual关键字后，变为虚继承
//此时公共的父类Animal称为虚基类
class Sheep : virtual public Animal {};
class Tuo   : virtual public Animal {};
class SheepTuo : public Sheep, public Tuo {};

void test01()
{
	SheepTuo st;
	st.Sheep::m_Age = 100;
	st.Tuo::m_Age = 200;

    //当菱形继承，两个父类拥有相同数据，需要加以作用域区分
	cout << "st.Sheep::m_Age = " << st.Sheep::m_Age << endl;  //100
	cout << "st.Tuo::m_Age = " <<  st.Tuo::m_Age << endl;  //200
	cout << "st.m_Age = " << st.m_Age << endl;//200
}
```

### 4.7 多态

允许父子之间的类型转换 不需要做强制类型转换

#### 4.7.1 多态的基本概念

多态——多种形态

多态是C++面向对象三大特性之一



**概念：**通过使用虚函数和指针或引用，实现对不同对象的操作，但通过相同的接口或抽象类进行调用（一个接口多种形态）

**分类：**

* 静态多态: 函数重载 和 运算符重载 属于静态多态，复用函数名
* 动态多态: 派生类和虚函数实现运行时多态

**区别：**

* 静态多态的函数地址早绑定  -  编译阶段确定函数地址
* 动态多态的函数地址晚绑定  -  运行阶段确定函数地址

**语法：**在基类的函数前加上virtual关键字，使其变成虚函数（子类函数virtual关键字可加可不加）

​          因为传的对象不同，不能一开始就绑定，多种形态调用接口 ，通过virtual实现运行阶段才绑定函数地址（晚绑定） 

**动态多态满足条件：**

* 有继承关系
* 子类重写父类中的虚函数

**动态多态发生条件：**

* 父类的指针或引用 执行子类对象

**多态的原理：**　

每个有虚函数的类在内存中都有一个vfptr(虚函数指针)，其指向一个vftable(虚函数表)，里面存放了该类所有虚函数的地址。当通过基类指针调用虚函数时，实际上是通过vftable来找到真正的函数地址并执行。

* 当一个Animal类中只有一个void函数时，size为1

  当一个Animal类中把这个void设成了虚函数时，size为4（vfptr的大小）

* 当子类重写父类的虚函数时，子类中的虚函数表内部才会替换成子类的虚函数地址（没重写时则是继承父类的内容）

```c++
class Animal
{
public:
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};
class Cat :public Animal
{
public:
	void speak()
	{
		cout << "猫在说话" << endl;
	}
};
class Dog :public Animal
{
public:
	void speak()
	{
		cout << "狗在说话" << endl;
	}
};
void doSpeak(Animal& animal) //父类的指针或引用 执行子类对象
{
	animal.speak();           
}
void test()          //通过不同对象对相同接口进行调用
{
	Cat cat;
	doSpeak(cat);
    
    Dog dog;
    doSpeak(dog);
}
```

#### 4.7.2 多态案例——计算器类

多态的优点：

* 代码组织结构清晰
* 可读性强
* 对于前期和后期的扩展以及维护性高

```c++
class AbstractCalculator
{
public:
	virtual int getResult()
	{
		return 0;
	}
	int m_Num1;
	int m_Num2;
};

//加
class AddCalculator:public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 + m_Num2;
	}
};
//减
class SubCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 - m_Num2;
	}
};
//乘
class MulCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 * m_Num2;
	}
};
void test()
{
	AbstractCalculator* abs = new AddCalculator;
	abs->m_Num1 = 10;
	abs->m_Num2 = 10;
	cout << abs->m_Num1 << "+" << abs->m_Num2 << "=" << abs->getResult() << endl;
	delete abs;

    abs = new SubCalculator;
	abs->m_Num1 = 10;
	abs->m_Num2 = 10;
	cout << abs->m_Num1 << "-" << abs->m_Num2 << "=" << abs->getResult() << endl;
	delete abs;

	abs = new MulCalculator;
	abs->m_Num1 = 10;
	abs->m_Num2 = 10;
	cout << abs->m_Num1 << "*" << abs->m_Num2 << "=" << abs->getResult() << endl;
	delete abs;
}
```

#### 4.7.3 纯虚函数和抽象类

虚函数的实现在父类中没意义，引入纯虚函数

* 纯虚函数语法：`virtual 返回值类型 函数名 （参数列表）= 0 ;`
* 类中有纯虚函数时称为**抽象类**
* 抽象类特点：
  * 无法实例化对象（不管堆区还是栈区）
  * 子类必须重写抽象类中的纯虚函数，否则也属于抽象类

```c++
class Base
{
public:
	virtual void func() = 0;
};
class Son :public Base
{
public:
	virtual void func() 
	{
		cout << "func调用" << endl;
	};
};
void test01()
{
    //创建了一个实际的对象（实例）
	Base  b;  // 错误，抽象类无法实例化对象
    new Base; // 错误，抽象类无法实例化对象
    
	//创建了一个指向对象的指针
	Base * base = new Son;
	base->func();
	delete base;//记得销毁
}

```

#### 4.7.4 多态案例2——制作饮品

**案例描述：**

制作饮品的大致流程为：煮水 -  冲泡 - 倒入杯中 - 加入辅料

利用多态技术实现本案例，提供抽象制作饮品基类，提供子类制作咖啡和茶叶

```c++
class AbstractDrinking
{
public:
		//煮水
		virtual void Boil() = 0;
		//冲泡
		virtual void Brew() = 0;
		//倒入杯中
		virtual void PourInCup() = 0;
		//加入辅料
		virtual void PutSomething() = 0;
		//制作饮品
		void makeDrink()
		{
			Boil();
			Brew();
			PourInCup();
			PutSomething();
		}
};
//制作咖啡
class Coffee :public AbstractDrinking
{
public:
	//煮水
	virtual void Boil()
	{
		cout << "煮农夫山泉" << endl;
	}
	//冲泡
	virtual void Brew()
	{
		cout << "冲泡咖啡" << endl;
	}
	//倒入杯中
	virtual void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}
	//加入辅料
	virtual void PutSomething()
	{
		cout << "加入糖和牛奶" << endl;
	}

};
//泡茶
class Tea :public AbstractDrinking
{
public:
	//煮水
	virtual void Boil()
	{
		cout << "煮矿泉水" << endl;
	}
	//冲泡
	virtual void Brew()
	{
		cout << "冲泡茶叶" << endl;
	}
	//倒入杯中
	virtual void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}
	//加入辅料
	virtual void PutSomething()
	{
		cout << "加入枸杞" << endl;
	}

};
void doWork(AbstractDrinking* abs)
{
	abs->makeDrink();
	delete abs;
}
void test01()
{
	doWork(new Coffee);
	cout << "------------------" << endl;
	doWork(new Tea);
}
```

#### 4.7.5 虚析构和纯虚析构

解决问题：多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码（**父类指针释放子类对象时不干净**）

解决方式：将父类中的析构函数改为**虚析构**或者**纯虚析构**



虚析构和纯虚析构共性：

* 可以解决父类指针释放子类对象
* 都需要有具体的函数实现

虚析构和纯虚析构区别：

* 如果是纯虚析构，该类属于抽象类，无法实例化对象



虚析构语法：`virtual ~类名(){}`

纯虚析构语法：

​       ` virtual ~类名() = 0;`          ——类内

​       `类名::~类名(){}`                      ——类外

注意：纯虚析构类外要有实现，因为父类可能也有一些属性要开辟到堆区，后释放

```c++
class Animal
{
public:
	Animal()
	{
		cout << "Animal 构造函数调用！" << endl;
	}
	//virtual~Animal()
	//{
	//	cout << "Animal 析构函数调用！" << endl;
	//}
	virtual void speak() = 0;
	virtual~Animal() = 0;
};
Animal::~Animal()
{
	cout << "Animal 纯析构函数调用！" << endl;
}
class Cat : public Animal
{
public:
	Cat(string name)
	{
		cout << "Cat构造函数调用!" << endl;
		m_Name=new string(name);
	}
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
	~Cat()
	{
		cout << "Cat析构函数调用!" << endl;
		if (m_Name != NULL)
		{
			delete m_Name;
			m_Name = NULL;
		}
	}
public:
	string* m_Name;
};
void test01()
{
	Animal* animal = new Cat("Tom");
	animal->speak();
	delete animal;
}
```

注：如果子类中没有堆区数据，可以不写为虚析构或纯虚析构

#### 4.7.6 多态案例三-电脑组装

**案例描述：**

电脑主要组成部件为 CPU（用于计算），显卡（用于显示），内存条（用于存储）

将每个零件封装出抽象基类，并且提供不同的厂商生产不同的零件，例如Intel厂商和Lenovo厂商

创建电脑类提供让电脑工作的函数，并且调用每个零件工作的接口

测试时组装三台不同的电脑进行工作

![](F:\大四学习\C++\image\微信图片_20231115142740.png)

## 5 文件操作

程序运行时产生的数据都属于临时数据，程序一旦运行结束都会被释放

通过**文件**可以将**数据持久化**

C++中对文件操作需要包含头文件 &lt; fstream &gt;



文件分类：

1. **文本文件**     -  文件以文本的**ASCII码**形式存储在计算机中

2. **二进制文件** -  文件以文本的**二进制**形式存储在计算机中，用户一般不能直接读懂它们

   

操作文件的三大类:

1. ofstream：写操作        ——将内容写（输出）到文件
2. ifstream： 读操作
3. fstream ： 读写操作



文件打开方式：

| 打开方式    | 解释                       |
| ----------- | -------------------------- |
| ios::in     | 为读文件而打开文件         |
| ios::out    | 为写文件而打开文件         |
| ios::ate    | 初始位置：文件尾           |
| ios::app    | 追加方式写文件             |
| ios::trunc  | 如果文件存在先删除，再创建 |
| ios::binary | 二进制方式                 |

**注意：** 文件打开方式可以配合使用，利用|操作符

**例如：**用二进制方式写文件 `ios::binary |  ios:: out`



### 5.1 文本文件

#### 5.1.1 写文件

写文件步骤：

1. 包含头文件   

   \#include <fstream\>

2. 创建流对象  

   ofstream ofs;

3. 打开文件

   ofs.open("文件路径",打开方式);    

4. 写数据

   ofs << "写入的数据";

5. 关闭文件

   ofs.close();

**注意：**

* 如果文件路径只是文件名，则默认在该.cpp文件同目录下
* 写文件可以利用 ofstream  ，或者fstream类

```c++
#include <iostream>
using namespace std;
#include <fstream>
void test01()
{
	ofstream ofs;
	
	ofs.open("test.txt", ios::out);
	
	ofs << "姓名：www" << endl;
	ofs << "年龄：21" << endl;
	ofs << "性别：女" << endl;

	ofs.close();
}
```

#### 5.1.2 读文件

读文件步骤：

1. 包含头文件   

   \#include <fstream\>

2. 创建流对象  

   ifstream ifs;

3. 打开文件并判断文件是否打开成功   `ifs.is_open()`

   ifs.open("文件路径",打开方式);

4. 读数据

   四种方式读取：（记住1-2种）

   * 第一种

     从输入流`ifs`中读取数据时，每次读取到一行数据的末尾，就会将这一行数据存储到`buf`数组中。

     ```c++
     char buf[1024] = { 0 };
     while (ifs >> buf)      //到输入流末尾或读取数据时发生错误时跳出循环
     {
     	cout << buf << endl;
     }
     ```

   * 第二种

     ```C++
     char buf[1024] = {0};
     while (ifs.getline(buf, sizeof(buf)))//到输入流末尾或读取数据时发生错误时跳出循环
     {
         cout << buf << endl;
     } 
     ```

   * 第三种

     getline（）是标准库函数，要加头文件 `#include <string>`

     ```c++
     string buf;
     while (getline(ifs, buf))
     {
     	cout << buf << endl;
     }
     ```

   * 第四种（不推荐）

     EOF代表文件尾

     ```c++
     char c;
     while ((c = ifs.get() != EOF)   
     {
     	cout << c;
     }
     ```

5. 关闭文件

   ifs.close();

注：

* 读文件可以利用 ifstream  ，或者fstream类
* 对文件进行操作时最好使用字符数组，减少使用string字符串

### 5.2 二进制文件

#### 5.2.1 写文件

 二进制方式写文件：文件输出流对象 通过write函数 写

函数原型 ：`ostream& write(const char * buffer,int len);`

​                    字符指针buffer指向内存中一段存储空间。len是读写的字节数

```c++
//写文件
    Person p = { "张三",18 };
	ofs.write((const char*)&p, sizeof(Person));
```

#### 5.2.2 读文件

二进制方式读文件：文件输入流对象 通过read函数 读

函数原型：`istream& read(char *buffer,int len);`

​                   字符指针buffer指向内存中一段存储空间。len是读写的字节数

```c++
ifs.open("Person.txt", ios::in |ios::binary);
Person p;
ifs.read((char*)&p, sizeof(Person));
cout << "姓名： " << p.name << " 年龄： " << p.age << endl;
```

