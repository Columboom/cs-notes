# c语言学习笔记

## c基础

- [c语言学习笔记](#c语言学习笔记)
	- [c基础](#c基础)
		- [标识符](#标识符)
				- [命名规则](#命名规则)
				- [属性](#属性)
		- [进制](#进制)
				- [进制转换](#进制转换)
				- [二进制的逻辑运算](#二进制的逻辑运算)
		- [运算符](#运算符)
		- [转换说明符Conversion Specifier](#转换说明符conversion-specifier)
				- [tips](#tips)
				- [常用标记](#常用标记)
		- [循环语句](#循环语句)
		- [if语句](#if语句)
		- [switch语句](#switch语句)
		- [数据类型](#数据类型)
				- [基本数据类型](#基本数据类型)
				- [其他](#其他)
				- [定义常量](#定义常量)
				- [自定义数据类型之一](#自定义数据类型之一)
		- [转义字符](#转义字符)
		- [printf](#printf)
		- [函数](#函数)
				- [常用函数](#常用函数)
				- [自定义函数](#自定义函数)
				- [其他](#其他-1)
		- [数组](#数组)
		- [指针](#指针)
		- [头文件](#头文件)
		- [结构体&共用体](#结构体共用体)
			- [结构体struct](#结构体struct)
				- [typedef](#typedef)
			- [共用体union](#共用体union)
				- [位域](#位域)
		- [数据结构简介](#数据结构简介)
			- [线性表](#线性表)
			- [（堆）栈](#堆栈)
			- [队列](#队列)
			- [树](#树)
			- [字典](#字典)
		- [文件](#文件)
				- [文件处理函数](#文件处理函数)
				- [文件类型指针](#文件类型指针)
		- [预处理](#预处理)
				- [预处理命令（4种）](#预处理命令4种)
				- [标准c中预定义的符号常量](#标准c中预定义的符号常量)
				- [断言语句](#断言语句)
		- [良好编程习惯](#良好编程习惯)


 > 主要参考资料
 > 1. 《c语言大学教程（第八版）》
 > 2. 郝斌c语言自学教程（bilibili）
 > 3. 浙大翁恺:程序设计入门——C语言（中国大学mooc）

### 标识符
##### 命名规则
- 字母、数字、下划线组成；
- 大小写敏感；
- 不能以数字开头；
- 不要以下划线开头，防止与系统标识符冲突；
- 一般第一个字母小写，否则其具有特殊含义；
##### 属性
- 存储类型
    - auto：声明局部变量（局部变量默认为auto）（不能声明数组）；
    - static：标识函数/全局变量/局部变量均可；（函数内用static修饰的局部变量(默认初始化为0)在函数结束时不会被释放；修饰的全局变量和函数只能在当前文件中访问使用）
    - extern：声明要使用的其他地方定义的全局变量（声明时数据类型可省略）（全局变量（若未初始化则默认初始化为0）和函数名默认为extern）；//?
    - register(历史遗留)
- 存储周期
	- 动态（只在相关程序块创建和释放）：auto/register；
	- 静态（程序运行之前就被一次性分配和初始化（默认为0））：static/extern；
- 作用域
	- 据此可把变量分为局部变量和全局（外部）变量；若全局变量与局部变量重名，在局部变量的范围内，局部变量有效，全局变量被“屏蔽”。
	- 函数作用域：标号标识符；
	- 文件作用域：在所有函数之外定义的标识符；
	- 程序块作用域：在一个程序块内部定义的标识符；
	- 函数原型作用域：函数原型形参列表中的标识符；

### 进制 
- 后缀标识：二进制标识B 十进制D可省略 八进制O 十六进制H 
- 前缀标识: 0表八进制  0x或0X表十六进制 
##### 进制转换
- 十进制转R进制，整数部分用除R取余数倒排法，小数部分用乘R取整顺排法 ；
- 二进制转八进制，三位合一位法；二进制转十六进制，四位转一位法；
- 八进制转二进制，一分为三法；十六进制转二进制，一分为四法 ；
##### 二进制的逻辑运算
- 或v相当于+；与∧相当于×；异或⊕相同为0不同为1；
  
### 运算符
- =表赋值；%表取余（取余结果与除数同号）；
- ++表加1，--表减1，置于前缀后缀均可，但单与其他运算符连用时，前缀表示改变自身再参与运算，后缀表示参与运算再改变自身；（一元运算符与操作数之间不要空格）
- a+=b 表示a=a+b,其他二元运算符同理；
 - 只能用（）更改算术运算优先级；
 - <=表小于或等于；>=表大于或等于；==表等于；!=表不等于 ；
 - &&表与；||表或；!表非（作前缀）； （短路求值：一旦能够确定表达式真值计算就会停止）；
 - 位运算符：&表按位与（转换成二进制补码逐位运算），|表按位或，~表按位取反，^表按位异或，<<表按位左移，>>表按位右移；
- 表达式的值为0即为假，非0均为真。
- 逗号运算符：多个表达式用逗号联接起来构成逗号表达式，从左往右依次执行，以最后一个表达式的值作为整个表达式的值。
- 条件运算符（三元）（若表达式真则去值1，否则取值2）：【表达式】？【值1】：【值2】
  
```c
#include <stdio.h>
//移位运算符应用：以int（32位）二进制输出数据；
void putbin(int n) {
	unsigned int flag = 1;
	flag <<= 31;
	for (; flag; flag >>= 1) {
		printf("%d", n & flag ? 1 : 0);
	}
	puts("");
}

int main(void) {

	int n = 0;
	scanf("%d", &n);
	putbin(n);

	return 0;
}
```

### 转换说明符Conversion Specifier
包括输出输入控制符for read or display datas

-    %c 字符 ，在中间插入*号可将其输入流丢弃
-    %i 有符号整数
-    %d 输出有符号十进制整数
-    %u 无符号十进制整数
-    %o 无符号八进制整数
-    %x 和 %X 无符号十六进制整数
-    h短 l长 ll长长 修饰整形转换说明符
-    %f 浮点数（输出默认四舍五入保留小数点后6位）
-    %e 和 %E 指数形式的浮点数
-    %g 和 %G 若浮点数幂值小于-4或大于等于该数打印精度则以指数形式，否则正常
-    l双精度 L长双精度 修饰浮点数
-    %s 字符串（接受的实参是指向字符的指针）
-    %p 地址值，输出时格式为十六进制的整数
-    %% 输出%或忽略一个输入的%
-    %n 在一个指向整型的指针中保存目前scanf已输入的字符总数  
##### tips
- 注意，输入float用%f，输入double或long double用%lf。输出float或double用%f，输出long double用%lf；
- 可在%和转换说明符之间用.【n】控制输出n位的精度
- 可在%和转换说明符之间用【n】来控制输入输出的n位字符的域宽，默认向右对齐；
- 可先用【*】代替上述的【n】，再在实参列表中指定
- `% [【字符组】] `扫描集，储存输入流中与上述字符相同的字符，当扫描到一个不同的字符即停止 ；在 【字符组】前加 ^号可创建逆向扫描集，即储存输入流中与上述字符不同的字符，当扫描到一个相同的字符即停止 ；
##### 常用标记
位于%右侧
- -：左对齐；
- +：显示正负号；
- #：输出整型进制前缀或输出浮点数小数点；
- 0：用0填满域宽；
- 空格：在没有打印+的正数前打印一个空格；
  
```c
#include <stdio.h>
int  main() {

	char c = 'z', a;
	int i = 100, i1, i2, i3, i4, i5, i6;
	float f = 2.22;
	double d = 33.345678901;

	//scanf( " %c\n %d\n %u\n %o\n %x\n %f\n %e\n",&c, &i1, &i2,&i3, &i4, &f, &d );
	//printf(" %c\n %d\n %u\n %o\n %x\n %X\n %#X\n %f\n %f\n %.9f\n %e\n %E\n", c, i1, i2, i3, i4, i4, i4, f, d,d,d,d);
	//scanf("");
	printf(" 1%c2  ", a);
	printf("  %p  ", f);
	printf("  %+d  ", i);
	printf("  %*.*f  ", 3, 4, d);
}
```

### 循环语句
- loop structures：while, do-while,for;
- `break;`和`continue;`均可用于其中； （break表退出循环；continue作用为终止当前循环迭代但不是整个的循环，在for中为跳过接下来的循环语句直接循环；）
-  格式：
   ` while (【expression】)    【statement】;`  
    `do   【Statement】   while ( 【Expression】 ) ;`  
    `for ( 【initialization expression】 ;  【test expression】 ; 【update expression】 )     【statement】;`  
- 循环中更新的数据勿定义为浮点型（不准确）
- 使用规律：有固定次数用for，必执行一次用do-while，否则用while

```c
#include <stdio.h>    //EX4_34.c

int main() {
	int row, col, height, width;
	char what;

	scanf("%d %d %c", &height, &width, &what);

	for ( row = 0; row < height; row++ ) {
		for (col = 0; col < width; col++ ) {
			printf( "%c",  what );
		}
		printf( "\n" );
	}

	return 0;
}

for ( r = 1; r <= 10; r++ ) {
	printf( "r:%d ", r);

	area = 3.14 *  r * r;

	if ( area > 100 )
		continue;

	printf( "area:%f\n ", area );
}

printf( "\n------------------\n" );
printf( "%f \n", area );

int t = 1;
for (;; t += 1) { //无限循环语句
	printf("Love you for %d years.\n", t);
}
```

### if语句
- if、if else、if else if else...else(连用可控制多选择支) 
- else 有最近匹配规则
```c
#include <stdio.h>  //EX4_20.c 
int main()
{   
	int  AQIndex ;
	AQIndex = 35 ;
	if  (60 < AQIndex < 80)//error;该语句相当于(60 < AQIndex) < 80即0<80; 应用&&；C uses short circuit evaluation of logical expressions. This means logical expressions are evaluated left to right and evaluation stops as soon as the final truth value can be determined.       
	    printf( "HEALTHY Hazard") ;
    return 0;
}
```

### switch语句
- 可控制多选择支
- 格式：
    ```c
    switch( 【IntegralExpression】 )
    {
    case 【Constant11】：
    case 【Constant12】：            （允许多个case并列，只需满足其中一个）
        【statement1】；
    break ；
    case 【Constant21】：
    case 【Constant22】：
        【statement2】；
    break ；
    ...
    default：                      （表默认选项，可删除）
        statement；
    break；                        （用于退出switch，末尾可省略）
    }
    ```
    优化片段（忽略输入流常见干扰字符）:
    ```c
    case '\n':
    case '\t':
    case ' ':
        break;
    ```

- 注意：case仅为程序入口，一旦找到入口所有case将屏蔽，故break一般不可省略！

### 数据类型  
##### 基本数据类型
  - char字符型 1字节 ；
  - int 整型 一个字 一般4字节（取决于编译器/cpu）  ； short (int)短整型2字节 ； long (int)长整型 一个字 4字节 （取决于编译器/cpu）；
  - float 单精度浮点型4字节  ；  double双精度浮点型8字节 ；
  - void 声明函数无返回值或无参数，声明无类型指针，显式丢弃运算结果；
  - size_t 无符号整型，推荐用于数组长度或下标变量；
  - const 修饰符，防止变量被修改； （在定义指针时，若在数据类型前则表常量数据，若在*号后则表常量指针）
  ##### 其他
 - 强制类型转换运算符（创建副本）：`(【数据类型】)【操作数】；`
 - 一元静态（编译时运行）运算符sizeof 可显示任何变量名、数据类型、数值的字节大小，若操作数为类型名则要用圆括号括起来； //e1
 - 符号常量CHAR_BIT（属<limits.h>）表一个字节所含二进制位数（标准值位8）；
  - 不要比较两个浮点数是否相等，可比较两者近似相等，因为浮点数的处理常会用精度丢失。
  - c语言允许将字符根据ASCII储存在整型变量中；//e4
##### 定义常量  
- 法一： 用const前缀修饰 //e2
- 法二（编译时程序语句中使用该标识符都会被其后的替换文本替换，如此使程序更易修改。）：` # define 【标识符名称】 【替换文本】 `  //e3
 （建议此标识符全大写以着重）

##### 自定义数据类型之一
- 定义枚举类型（元素为标识符，其值依次增1，若不赋值则首个默认为0）:
    `enum 【枚举名】 {【元素1】=【n】,【元素2】,...};`
    （建议元素命名全用大写以着重；标识符不可重复，但其值可重复；）
    定义该类型的变量：`enum 【枚举名】 【变量名】；`
```c
#include <stdio.h>
# define e 2.7  //e3  
int main() {
//e1
	printf( "size of int is: %d \n", sizeof( int ) );
	printf( "size of float  is: %d \n", sizeof( float ) );
	printf( "size of short is: %d \n", sizeof( short ) );
	printf( "size of long is: %d \n", sizeof( long ) );
	printf( "size of char is: %d \n", sizeof( char ) );
	printf( "size of double is: %d \n", sizeof( double ) );
//e2
	const float PI = 3.14;
	//PI++ ;//error
	printf("PI = %f \n", PI) ;
	printf("e=%f \n", e);
//e4
	printf("%c %d", 'a', 'a');
}
```

### 转义字符

 Escape Sequences转义序列： （部分）
-    \a 响铃(BEL) //e4
-    \b 退格(BS) //e3
-    \f 换页(FF)，将光标移到下页开头      ？
-    \n 换行(LF) //e2
-    \r 回车(CR) (将光标移到本行开头)//e1
-    \t 水平制表（将光标移到下个制表位置） //e7
-    \v 垂直制表
-    \\ 插入一个反斜线 //e5
-    \" 插入一个双引号 //e6
-    \' 插入一个单引号
-    \? 插入一个问号
-    \0 插入一个空字符(NULL)

```c
#include <stdio.h>
int main() {
	printf("1\r2") ;//e1
	printf("3\n4") ;//e2
	printf("55\b6") ;//e3
	printf("\a") ;//e4
	printf("nn\\nn\"nn") ;//e5 e6
	printf("xxx\tyyy\tzzz\n1\t2\t3");//e7
}
```

### printf
 - 用法一 ：printf("【字符串】");//e1
 - 用法二 ：printf("【...输出控制符1...输出控制符2...】", 【输出参数1】, 【输出参数2】, ...);//e2

- 输出字符串时遇\0而止；
```c
# include <stdio.h>
int main() {
	puts(" HELLO C ");//e3
	printf(" HELLO WORLD ");//e1
	char x = 'a', y = 'b', z = 'c';
	printf("...%c...%c...%c...", x, y, z ); //e2
}
```

### 函数

##### 常用函数
- 数学函数库`<math.h>`:
	- `pow(x,y)`表x的y次幂，返回值类型为double；
	- `abs()`整型绝对值；`fabs()`浮点型绝对值；
	- `sqrt()`开平方
	- `log()`求自然对数； `log10()`求常用对数；

- 时间函数库`<time.h>`：
	- `time(NULL)`返回以秒为单位的1970年至今经历的时间；


- 字符处理函数库`<ctype.h>`（以整型接受单个字符或EOF）：
	- `toupper()`若操作数为单个小写字母，将其改为大写字母；`tolower()`反之；
 	- `is...()`判断是不是...；

- 通用工具函数库`<stdlib.h>` :  //e？
	- `rand()`生成随机数 ；`srand()`结合前者使用，从键盘读取一个种子使得每次生产的随机数都不同，或使用`srand(time(NULL))`自动读取计算机时钟值作为种子；
	- (程序调试时建议先删掉srand)//why???
	- `strtod(【字符串】,【指向该字符串的指针】)`将字符串转换为double，不能转换的部分字符串赋给指针，失败则返回0；
	- `strtol(【字符串】,【指向该字符串的指针】,【基数】)`将字符串转换为long，不能转换的部分字符串赋给指针，失败则返回0；
	- `strtoul(【字符串】,【指向该字符串的指针】,【基数】)`将字符串转换为`unsigned long`，不能转换的部分字符串赋给指针，失败则返回0；
	- `strtoll(【字符串】,【指向该字符串的指针】,【基数】)`将字符串转换为`long long int`，不能转换的部分字符串赋给指针，失败则返回0；
	- `strtoull(【字符串】,【指向该字符串的指针】,【基数】)`将字符串转换为`unsigned long long int`，不能转换的部分字符串赋给指针，失败则返回0；
	- `malloc(【字节数】)`在堆区动态申请一块指定大小的内存空间并以void*形式返回（可以说无作用域和生命周期限制）；
	- `realloc(【指针名】,【新字节数】)`将该指针指向的动态内存空间扩大/缩小成新字节数；
	- `free(【指向void的指针】)`释放指定动态内存空间；

- 标准输入输出库`<stdio.h>` : //e?
	- `fgets(【字符数组名】,【最多输入字符个数】,stdin)`不断从键盘读入字符并储存在指定数组中直到换行符或EOF或满溢；
	- `getchar() putchar()`读取或打印一个字符
	- `sprintf(【字符数组名】,"【相应格式】",【数据名】)` 将格式化的数据存入指定字符数组中
	- `sscanf(【字符数组名】,"【相应格式】",&【数据名】,...)`将字符数组中数据取出并按格式存入后续数据名中
	- `printf() scanf()`
	- `puts("【字符串】")（会自动换行）；gets(【字符串名】)`（读取到回车为止并返回）；

- 字符串处理函数库`<string.h>`:（处理至字符串中的第一个结束符时结束，并不一定处理全部字符）
	- strcpy/strncpy复制
	- strcat/strncat拼接
	- strcmp/strncmp比较
	 （上述后者为安全版本，多加一个限制操作字符个数的参数）
	- strlwr转小写
	- strupr转大写
	 strlen返回字符串长度
	- `strchr(【字符串指针】,【特定字符】)`查找第一个指向指定字符的指针（反向查找strrchr）；
	- `strstr(【字符串指针1】,【字符串指针2】)`返回字符串2在字符串1中首次出现的位置；
	- `strcspn(【字符串指针1】,【字符串指针2】)`查找字符串1中一段不包含字符串2中任一字符的片段，返回该片段的长度；
	- `strspn(【字符串指针1】,【字符串指针2】)`查找字符串1中一段只包含字符串2字符的片段，返回该片段的长度；
	- `strpbrk(【字符串指针1】,【字符串指针2】)`确定字符串2中任一字符在字符串1中第一次出现的位置，返回其指针；
	- `strtok(【字符串指针】,【特定字符】)`用特定字符将字符串分割，后面每一次NULL调用，都会将一个分隔符置为`\0`，然后返回首字符指针，实现分字段输出；//e1

 - 内存处理函数
 	- `memcpy(【字符串指针1】,【字符串指针2】,【字符数n】)`将字符串2中的n个字符复制到字符串1中并返回字符串指针1；
 	- `memmove(【字符串指针1】,【字符串指针2】,【字符数n】)`将字符串2中的n个字符复制到一个临时数组中再复制到字符串1中并返回字符串指针1（故允许同一个字符串中的复制）；
 	- `memcmp(【字符串指针1】,【字符串指针2】,【字符数n】)`比较两字符串前n位，返回正负零；
 	- `memchr(【字符串指针】,【字符】,【字符数n】)`在字符串前n位查找第一个指向指定字符的指针；
 	- `memset(【字符串指针】,【字符】,【字符数n】)`将字符串前n位都替换为指定字符并返回字符串指针；
- 其他函数
	- strlen计算字符串长度
	- strerror
#####  自定义函数
格式（第一行被称为函数头）：
    ```
	 【返回值类型】 【函数名】(【接收值类型】 【接收值名称1】,【接收值类型】 【接收值名称2】,...)
	 {【语句】}
    ```
##### 其他
- 函数不能相互嵌套
- 在主程序中预先输入函数原型：`【自定义函数头】;`可使编译器检查函数是否被正确调用，可实现实参类型强制转换；
- 在返回void的函数内使用语句`return;`，可直接退出函数；
- 递归函数必需返回值；
- main函数可带形参，通常为`(int argc,char *argv)`，后者为一字符串数组，前者为该数组元素个数，字符串实参从命令行中读取；
```c
#include <string.h>
#include <stdio.h>
//e1
int main(void) {
	char input[16] = "abc,de,f";
	char *p;
	p = strtok(input, ",");
	if (p)
		printf("%s\n", p);
	p = strtok(NULL, ",");
	if (p)
		printf("%s\n", p);
	return 0;
}
```

### 数组
- 定义并初始化（若省略元素个数则默认为初始化个数，若初始化个数少于元素个数其余元素自动初始化作0）：`【数据类型】 【数组名】[【元素个数】] ={【元素1】,【元素2】,【元素3】,...} ;`
- 数组中的字符串均以\0结尾；元素为字符时可直接定义为（计算机会自动补上结尾\0）：` char 【数组名】 [] ="【字符串】" ;`
- 字符串连用会自动合并成一个大字符串；
- 指定数组内某个元素（从0开始标序）： `【数组名】[【元素位序】]`
- scanf函数读取字符串时不需要取地址符&，直到读到空白字符或EOF为止，故要规定域宽来防止安全漏洞；(EOF热键：win中为`CTRL+Z`，Linux/UNIX中为`CTRL+D`；)

- 双下标数组（数表）定义和初始化（可省略内花括号）：` 【数据类型】 【数组名】[【行数】][【列数】] ={{【元素11】,【元素12】,【元素13】,...},{【元素21】,【元素22】,【元素23】,...},...} ;`

- 函数定义的形参列表中的数组第一个下标可省略，剩余下标必填；

- c99：
	- 允许定义可变长度数组；
	- 允许初始化列表中的个别元素初始化（若省略元素个数则默认为最大的初始化个数，其余元素自动初始化作0）：`【数据类型】 【数组名】[【元素个数】] ={[【下标1】=【元素1】,【下标2】=【元素2】,...} ;`

- 将整个数组传递给函数时由于是传址，固该函可修改该数组各元素的值；

- 注意：
	- 空字符：`\0`；
	- 空白字符：空格、制表符、换行符（创建新行）、回车符、换页符、垂直制表符等；
	- `\0`字符和NULL字符的ASCII码均为0，空格字符的ASCII码非0；数字字符不等于数字；
```c
#include <stdio.h>
int main() {
	char s[3];
	scanf("%3s", s);
	printf("%s", s);
}
```

### 指针
e？
- 本质：变量地址
- 声明或调用其值：指针变量名前加上*号（间接寻址/解引用运算符）；
- 必须初始化为符号常量NULL、0或一个地址；
- &和*为互补运算；
- 数组名默认为指向数组首元素的可变数据的常量指针；函数调用数组时，在形参列表中声明为a[]，在实参列表中相应填入该数组名，使用时以a为数组名即可；
- 函数名就是其代码在内存中的起始地址，函数调用函数时，在形参列表中需声明为指针：`【被调用函数返回值类型】(*【指针名】)(该函数形参列表)`，在实参列表中相应填入该函数名，使用时需以`*【指针名】`为函数名；函数指针常应用于“基于文本的菜单驱动的系统”；
- 数组内的指针可与指针或整数进行加减运算，以所指对象的字节长度为运算单位；
- 同型指针可以直接赋值，void除外；非同型需用前缀`cast(【指针类型】)`强制转换；
- 指向void的指针不能被直接解引用，需先进行类型转换（如`*((int*)ptr)`）;
- 定义以指向一类函数的指针为元素的数组：`【该类函数返回值类型】(*【数组名】[【元素个数】])(该类函数形参列表)`，使用时用`(*【数组名】[元素次序])(函数形参列表)`
- 传递指针可变相实现函数返回多个值；
- 若以字符串初始化指针，则该字符串存放在堆区，只读不写；

### 头文件
e？
- 程序中一些代码可以独立储存在一个后缀为`.h`的文件中，如typedef定义语句、常量、枚举类型声明、函数原型等。
- 在用户程序加上`#include <文件名.h>`即可（自定义的头文件要将<>改为""）;
- `.h`文件还可分解为`.h`和`.c`两个文件；

### 结构体&共用体
e？
#### 结构体struct
- 本质：一组相关变量的集合，属派生数据类型；
- 定义格式：`struct 【结构体标记（命名）】{【数据类型1】【变量名1】;【数据类型2】【变量名2】;...};`
- 一个结构体不能包含其自身类型的变量，但可包含指向自身类型的指针变量（自引用）；
- 结构体变量定义和初始化（默认为0或NULL）：`struct 【该结构体标记】 【变量名】={...,...};`
- 若省略结构体标记，只能在定义结构体的同时定义结构体变量（紧随其后）；
- 由于结构体中的成员不一定被连续储存，固不能比较两个结构体类型变量是否相等；
- 初始化还可以通过赋值语句实现；
- 结构体变量默认以按值传递给函数；固可创建一个以数组为成员的结构体实现数组的按值传递；
- 访问结构体类型变量内的成员
  - 结构体成员运算符/圆点运算符：`【该结构体变量名】.【成员名】`;
  - 结构体指针运算符/箭头运算符：`【指向该结构体变量的指针名】->【成员名】`;
  （不要在以上运算符两边加空格，以强调整体性）
##### typedef
- 关键字typedef（可提高程序可移植性可读性可维护性）为已定义的数据类型创建同义词（建议别名首字母大写以着重）：`typedef【数据类型】【别名】;`
- 用typedef可省去结构体标记；

#### 共用体union
- 类似结构体，只不过所有成员共用一个储存空间，故每次只允许访问一个成员；
- c11支持在结构体共用体的嵌套，内层的常为无名的，可从外层直接访问；

##### 位域
- 对结构体或共用体中的整型成员可以指定其储存二进制位数（后缀:【位数】）；
- 指定宽度为0的无名位域可跳过上一个成员的储存单元中的剩余数位；
- 虽然使用位域可节约空间(还便于对数据的指定位作修改)，但会降低运行速度；

### 数据结构简介
#### 线性表
- 顺序表：元素顺序排列，需增删则后移；
- 链表：
    -   一组自引用（“链接”指针）结构体对象（节点）的线性排列
	-	指向首节点指针通常名为head；
	-	链接指针通常名为next，指向下一节点（尾节点中需指向NULL）；

#### （堆）栈
特殊的链表，新节点只能在顶部压入（push）或弹出返回（pop），后进先出，只能通过指针访问顶部节点；  

#### 队列
相对于栈，先进先出；

#### 树
一种非线性二维的数据结构
- 对二元数（常用于消除冗余/搜索），常用3种遍历方式（还有层序遍历等）：
	-	中序inorder：中序遍历左子树→处理节点中的值→中序遍历右子树；
	-	先序preorder：处理节点中的值→先序遍历左子树→先序遍历右子树；
	-	后序postorder：后序遍历左子树→后序遍历右子树→处理节点中的值；
- 二叉排序树BST：其左子节点<该结点<其右子节点
- 线索二叉树：根据指定的遍历方式，将空的指针域指向该顺序的前驱或后继结点（称为线索），使得再次遍历时节省时间
- 平衡二叉树（AVL树）：
	-	满足左子树和右子树深度之差的绝对值不大于1，且左子树和右子树也都是平衡二叉树；
	-	结点的左子树的深度减去其右子树深度称为该结点的平衡因子；

#### 字典
可以通过全需中的一个关键码来定位对应的数据；

`对于检查参数异常，c中可用assert，cpp常调用异常机制；`

### 文件
内容是顺序的字节流，以特定字节数或EOF结束；可永久保存数据；

- 流提供了文件与程序之间信息交换的通道；

- 每当程序开始执行，三个文件被自动打开：标准输入流（指针为stdin）、标准输出流（stdout）和标准错误流（stderr）；

- 打开一个文件将会自动一个返回指向FILE结构体类型（属`<stdio.h>`）的指针；
  
- 随机存取文件：其中各记录字节长度固定（可用结构体包装），便于修改；
##### 文件处理函数
- `fgetc(【文件指针】)` 从文件中读入一个字符；成功则返回该字符的整型值，否则返回EOF（-1）；
- `fputc(【单字符】,【文件指针】)` 向文件中写入一个字符；成功则返回该字符的整型值，否则返回EOF（-1）；
- `fgets(【字符数组指针】,【字符数】,【文件指针】) `从文件中读入指定数目的一行字符并储存在指定字符串中；成功则返回相同的该字符数组指针，否则返回NULL；
- `fputs(【字符数组指针】,【文件指针】) `向文件中写入一个字符串；成功写入一个字符串后文件的位置指针会自动后移，函数返回值为非负整数；否则返回EOF(值为-1)。
- `fopen(【文件名（若位置在不同目录则需加上路径）】,"【文件打开模式】")` （创建并）打开文件；成功则返回该文件指针，否则返回NULL；
- `feof(【文件指针】) `检查文件结束标记的存在，返回真假值；
- `fscanf() `相比`scanf`需多接受一个文件指针；从文本文件读入数据；成功则返回读取的数据个数，否则返回EOF；
- `fprintf()` 相比`printf`需多接受一个文件指针；向文件写入文本数据；
- `fclose(【文件指针】)` 关闭文件；（程序结束时会自动关闭所有文件）
- `rewind(【文件指针】)` 文件偏移量（文件位置指针）重置为0；
- `fwrite(【内存地址】,【数据字节长度】,【数据个数】,【文件指针】) `将内存中的多个数据直接以二进制写入文件中；成功则返回的数据个数，否则返回EOF；
- `fread() `与`fwrite`相反；
- `fseek(【文件指针】,【偏移量】,【起始位置】)` 设置文件偏移量；成功返回0，否则返回非0；（起始位置：`0`或`SEEK_SET`表文件开头位置，`1`或`SEEK_CUR`表当前位置，`2`或`SEEK_END`表文件末尾位置）

##### 文件类型指针
```c
typedef struct
{   short level;// 缓冲区程度
    unsigned flags;// 文件状态标志
    char fd;// 文件描述符
    unsigned char hold;// 如无缓冲区不读取字符
    short bsize;// 缓冲区大小
    unsigned char *buffer;// 数据缓冲区位置
    unsigned char *curp;// 数据指针
    unsigned istemp;// 临时文件标志
    short token;// 内部使用
}  FILE; // 文件结构
```

### 预处理

##### 预处理命令（4种）
均以`#`开头，编译器在编译程序之前处理，且对空白字符忽略；
1. 将其他文件的副本包含到正在编译的文件夹中；
2. 定义符号常量和宏；
	- 符号常量相当于不带参数的宏；
  	- 定义用`#define`，撤销用`#undef`；
  	- `#`运算符表示将要替换标记的字符串用双引号括起来；
  	- `##`运算符表示将要替换标记的字符串拼接起来；
  	- 若换行需在末尾加宏连续符`\`；
  	- 宏内可嵌套其他宏；
  	- 最好用函数取代宏；
3. 程序代码的条件编译；
 	- `#if !define...`和`#endif`用于防止重复define；
  	- `#if 0`和`#endif`用于注释；
  	- `#ifdef DEBUG`和`#endif`用于包含调试程序时需要printf的语句；
4. 有条件地执行预处理命令；
  	- `#erro【标记符】`打印标记符代表的信息并终止程序；
  	- `#pragma 【标记符】`执行标记符代表的操作；
  	- 标记符由系统实现决定；
  	- `#line 【整数】【文件名】`表示后续代码行数从指定整数开始编号且文件名改为指定文件名


##### 标准c中预定义的符号常量
- `_LINE_` 当前代码行号
- `_FILE_` 当前文件名
- `_DATE_` 当前源文件被编译的时期
- `_TIME_` 当前源文件被编译的时间
- `_STDC_` 若编译器支持标准c则其值为1否则0

##### 断言语句
- `<assert.h>`中定义了宏`assert(【表达式】)`；
- 若表达式值为0则打印出错信息（含当前行号和文件名）并调用`abort()`函数终止程序；
- 尽量在函数中使用它来检查参数的合法性；
- 默认情况下，assert只在 Debug 版本中才能起作用，而在 Release 版本中将被忽略。因此要避免在断言表达式中使用改变环境的语句。
- 为减少开销，调试结束后可在其前插入语句 `#define NDEBUG` 来禁用assert；

### 良好编程习惯
- 对每个函数、每个程序注释；
- 统一缩进；
- 变量命名有意义；
- 逗号后面加空格；
- 二元运算符两边加空格；
- 赋值语句中计算位于等号右侧；
- 最小权限原则；（如将函数原型声明在需要调用它的函数内）
- 为防止遭恶意估计，不要使用用户输入的字符数组作为转换说明符，多用puts或%s输出字符串；
- 空缺的形参列表在c++中视为void而在c中则允许传递任何类型实参，固这在c中是危险的；
- main函数末尾c++默认return 0而c不会固前者可省略该语句；
- 程序员应该根据正确的软件工程原则编写代码，将优化问题留给编译器，永远不要猜测编译器将来会变成什么样子；
- 尽量避免使用全局变量和静态本地变量，对线程不安全；

