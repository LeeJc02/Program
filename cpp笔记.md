```c++
#pragma once 在头文件中声明，避免预处理命令（头文件）被多次编译出错【部分编译器不支持】
    类比于#ifdef、#ifndef、#define、#endif对预处理命令的作用，#pragma速度更快
C++常用头文件(不加h):
#include<iostream>        标准输入输出流类：cin cout
#include<cstdio>          使用C语言的stdio库：printf scanf
#include<cmath>           使用C语言的math库
#include<ctype>           使用C语言的ctype库
#include<algorithm>       max min sort
#include<string>          string类
#include<cstring>         使用C语言的string库
#include<bits/stdc++.h>  （万能头，速度慢，oj专用）
```

```c++
二进制码：
    原码：二进制表示数据，最高位为符号位，1Byte最多储存2^7-1=127的数
            【原码存在+0和-0的二义性，不适用储存】
    反码：【除符号位之外】按位取反，仍具有二义性
    补码：正数补码即原码
          负数补码为反码+1，溢出舍去最高位
            【不存在二义性，用于计算机储存】
    阶码：机器数中【浮点数】的二进制指数 
            -----> N=2^p+S     N为浮点数，S为科学计数法小数，P为二进制指数
        阶符：p为正则0，负则1    阶数：p，即阶码 -----> 阶数确定为定点数，不确定为浮点数
        数符：S为正则0，负则1    尾数：S，即N的科学计数法表示、
    移码：补码的符号位取反【用于数的比较和阶码】
    无符号数：不参与计算，仅可进行逻辑按位运算，不可进行算术运算
              【多用于编码格式】

BCD码【仅作了解】

二进制转化：----> 八进制：二进制每3位表示的数==八进制每1位表示的数
           ----> 十六进制：二进制每4位表示的数==十六进制每1位表示的数
    二进制转化也可通过十进制进行中转转化
    二进制：0b开头
    八进制：0开头
    十六进制：0x开头
【注:高进制转低进制时，是先求低位再求高位，存储时以【栈】的形式存储，先进后出】
```

```c
简单的编译原理：（gcc/g++/MinGW）
    【  .c/.cpp ---> .i ---> .s ---> .o ---> .exe  】
由.c->.o的过程称为编译（compile）
    .c/.cpp         所编写的程序文件
    .i              头文件、定义宏展开的程序文件 
    .s              解析成汇编文件
    .o              目标文件（object）
由.o->.exe的过程称为链接（link）
    .exe            可执行文件（以二进制乱码储存）
```

![0s0527042663IMG_20230325_142834_edit_203598534905](C:\Users\86180\Documents\Tencent%20Files\407981034\FileRecv\MobileFile\0s0527042663IMG_20230325_142834_edit_203598534905.jpg)

```c
int 4字节32位 =2^31-1 ≈2×10^9    short 2字节16位 =2^15-1 ≈3×10^4
long 32位编译系统：4字节，同int    64位编译系统：8字节，同long long
long long 8字节64位 =2^63-1 ≈9×10^18

```

```c
数据类型转换： 
    （低）char -> short ->int -> long -> float -> double （高）
        可由高到低，隐式转换（损失精度） 也可由低到高（强转） 
十六进制输出：hex
八进制输出：oct
十进制输出：dec
二进制输出： 【将c转化为二进制字符串a】
             #include <bitset> bitset<sizeof(int)*8>a(c); -----> sizeof算一共所需的内存长度                                     
             cout<<a;
```

```c
signed：只能修饰整形，整形默认为此类型，算术位运算
unsigned：只能修饰整形，逻辑位运算
    算术/逻辑左移：高位溢出，低位补0
    算术右移：低位溢出，高位补符号数
    逻辑右移：低位溢出，高位补0
实型：
    可用E+/-n表示为×10^(n/-n)，科学计数法表示
    未声明默认为double类型，末尾加f/F则表示float类型
常量限定：
    以const int a限定一个整型常量a，也可写作const a，表示a的值不可修改，且为静态生存期，作用域不变
    【比#define方便快捷，利于修改】
引用：用于减少拷贝和指针作用，直接取地址，不占内存
    const和引用结合使用：仅可权限向下或平移继承，不可扩大权限
    也不可隐式转换放大权限
连续赋值运算：
    不加括号即报错

逻辑：&&与    ||或    ！非
按位： &与     |或    ~反        ^异或（相同为0，不同为1）o'non数据类型转换：
    （低）char -> short -> int -> long -> float -> double （高）
可由高到低，隐式转换（损失精度）    也可由低到高（强转）

十六进制输出：hex
八进制输出：oct
十进制输出：dec
二进制输出： 【将c转化为二进制字符串a】
    #include <bitset>
    bitset<sizeof(int)*8>a(c);  -----> sizeof算一共所需的内存长度
    cout<<a;
```

```c
杨辉三角数学版打印：
    每一遍循环：
        1.先打印1
        2.for(j=1,c=1;j<=i;j++){
            c = c*(i-j+1)/j;
            打印c的值
```

```c
字符库函数（cctype 对应C语言的ctype.h）
    判断函数：
        isalnum():判断字母/数字
        isalpha():判断字母
        isdigit():判断十进制数字     --->    isxdigit():判断十六进制数字
        islower():判断小写           --->    tolower():转化为小写
        isupper():判断大写           --->    toupper():转化为大写
        isspace():判断空白符（空格，回车，tab）
        isblank():判断空格符
（伪）随机库函数（random头文件/cstdlib头文件）
    rand():产生一个0到最大值的随机函数  
    通常与srand(time(0))【ctime库中函数
```

```c
自定义函数：
    - 形参不改变实参，注意函数使用变量的可见性
            局部变量仅可通过[指针/引用]进行更改（地址传参）
    - 函数可有默认值
            默认值参数必须放在其他参数之后
    - 内联函数：
            1.适用于函数体很小，使用频率高的【减少调用时花费】
            2.以inline关键字声明函数为内联函数，属于一个【编译命令】
            3.内联函数即在编译时将函数体【嵌入代码】，不进行调用花费
            4.不能进行【异常接口声明】，函数体不能有复杂结构和switch
    - 函数重载：
            1.多态函数，即【函数名】相同，通过【传参不同】自动选择函数
            2.重载必须参数表不能完全相同，即【形参类型、个数】，至少有一个不相同
    - 函数模板：
            1.相同运算法则的重载函数需要分别定义，以一个模板减少相同工作
            2.仅有【参数、函数类型】不一样
            2.template<typename T>    则T代表所有【基本数据类型】
            3.T add(T a,T b)    以T作为数据类型模板，仅需要定义一个函数
```

```c
main()函数：【C99标准】
    无参数形式：
        int main()                            大部分编译器合法，部分系统不合法
        int main(void)                        int main()的全写形式，参数为空（默认）
    有参数形式：
        int main(int argc,char *argv[])       参数由【系统传入】，是Unix系统标准写法
    argc：传入命令行参数个数        argv：传入参数的指针数组，每一个包含一个传入的参数
return：
    返回一个值（int/char/double/void）并结束函数
    返回给系统一个值：返回为0则程序正常结束
```

```c
数组：
    数组溢出:覆盖系统数据，导致出错
    数组初始化：
            - 声明数组时，数组下标只能为常量表达式
            - 静态数组默认为0，自动/动态数组需要初始化为0
            - 声明数组时必须明确数组个数，以便分配内存
            - int a[]类型的声明必须以花括号进行赋值定长度
    数组赋值:
            - 数组必须明确个数
            - 数组元素不能为空
    二维数组[行][列]:
            - 声明时同一维数组
            - 行的下标可省略，列的下标不可省略
            - [m][n]即为第m×n+n-1个元素【指针常用】
    二维数组的实质：
            - [行]储存的是指向[列]的指针，实际上是一个【储存指针】的一维数组
                    即arr指向arr[0]【一个指针】,arr[0]指向arr[0][0]   
                    字符串指针同理 
            - 二维数组指针，即二级指针（以**声明和访问）
                    二维数组名arr相当于一个指向指针的【二级指针】
    数组传参：
            - 传入的为该数组的首地址，可进行数据更改
            - 形参和实参共用数据和存储空间   
```

```c
字符串操作（cstring头文件）
    【传入s1，s2皆为指针传入】
    strlen(s):计算\0之前的字符串长度
    memset(s,c,n):将s中前n个字符赋值为c【常用于数组清零】
    strcmp(s1,s2):将s1与s2进行字典序比较，s1>s2则返回1    【strncmp，第三个参数为操作的字符串个数】
    strcat(s1,s2):将s2追加到s1                           【strncat，第三个参数为操作的字符串个数】
    strcpy(s1,s2):将s2复制到s1                           【strncpy，第三个参数为操作的字符串个数】
    【拓展】
    strchr(s,ch):查询s中【第一次】出现ch字符，成功返回ch地址，失败返回NULL
      - memchr(s,ch,n):在前n个字符中查询s中【第一次】出现ch字符，成功返回ch地址，失败返回NULL
    strrchr(s,ch):查询s中【最后一次】出现ch字符，成功返回ch地址，失败返回NULL
    strstr(s1,s2):查询s2是否为s1字串，成功返回s2在s1中的地址，失败返回NULL
    atoi(s):将s中的字符转化为int整形，遇到+/-/数字才开始转换，遇到非数字停止
      - 若转化超出int，则返回INT_MAX，若为负数转化，则返回INT_MIN
```

```c
超好用的algorithm：

    max/min():将括号内两个数进行求最大/最小值，如果为多个数以{}包含进去
    数组最大/最小值求法：
        max_element(arr,arr+n)
        min_element(arr,arr+n)
        【返回为地址，通过*可访问值，通过-arr获取位置下标】
    sort(arr,arr+n): 无返回值，默认将arr以【小-->大】排序
        sort(arr,arr+n,greater/less<int>())
        int为排序数据类型，可更换
        less为【小-->大】（默认）；greater为【大-->小】
```

```c
时间复杂度【大O阶】
    总运行语句数，最高次项且参数为1，即为时间复杂度
排行：
  O(1)【常数阶】-->O(lgn)【对数阶】-->O(n)【线性阶】-->O(nlgn)-->O(n^2)
        三阶及其以上复杂度太高，不予使用
```

```c++
自定义数据类型：结构体【struct】，枚举【enum】，共用体【union】，类型自定义【typedef】，类【class】
    自定义数据类型声明不分配内存，定义才分配
struct/enum/union声明格式：
    【  struct/enum/union <类型名>{  众成员  }<定义该数据类型变量>;  】
        若无<类型名>----匿名类型，仅可在声明时进行定义，之后不可再使用该类型结构
        众成员----【枚举-字符】【结构体-基本/自定义数据结构】【共用体-基本/自定义数据结构】
        若无<定义该数据类型变>----则可后面【通过<类型名>进行定义】

enum枚举变量：指的是枚举成员中某一个的值【仅可以符号赋值】
struct结构体变量：指的是结构体成员所有共同存在
union共用体变量：指的是共用体变量相互覆盖赋值（相当于一个多功能数据类型）
```

```c
enum枚举类型：【唯一一个能以符号代替数据的数据类型】
    enum Days { 成员 } today;
 声明一个名为Days的枚举类型，并定义一个Days类型的枚举变量today
    枚举中的符号与其【索引】值绑定，默认【从0开始】索引，若有额外赋值，则以赋值点开始往后递增
 枚举值【索引值】和枚举符号可相互转换：
        枚举值 -----> 用(enum Days)对值进行强转 -----> 得到索引符号【多用于switch】
        枚举符号 -----> 赋值给枚举变量 -----> 枚举变量储存的为对应的枚举值
```

```c
typedef类型自定义
    【  typedef 数据结构声明 <重命名>  】
    将某种基本/自定义数据结构，重新命名为一种类型，【只改变名称】
```

```c
struct结构体
    结构体变量初始化：
        - 可位置传参，也可访问结构体成员变量进行赋值
        - 结构体类型声明不可初始化
        - 同一类型的结构体，可相互赋值，成员一一对应
    结构体数组 -----> data/ *next ------> 【链表】
    内存：结构体变量的内存 == 结构体成员变量总内存之和，通常为【最大纯量】的倍数
```

```c
union共用体
    同一段空间储存不同类型的数据，成员之间相互覆盖，只有一个有效
    内存：共用体变量的内存 == 共用体成员变量之中的最大内存，通常为【最大纯量】的倍数
        "通常为【最大纯量】的倍数"指存储时需要内存对齐
```

```c
复合类型：    成员数据类型：    存储空间：    
 数组          必须一致          连续
 结构体       可以不一致         连续
 共用体       可以不一致         共用
 枚举          必须一致           
 链表          必须一致         非连续
  类         大概率不一致       不同成员函数不同存储
                               调用成员函数时调用公共存储的代码块
```

```c++
class类 ------ 面向对象编程(OOP)
    【C++基础不做重点，详情请见C++面向对象编程笔记（如果没有那就是我没做）】
    面向对象三大特征：1.继承 ---> 子类【派生类】继承父类【基类】的成员
                     2.多态 ---> 在继承的基础上，实现同一个类数不同作用
                     3.封装 ---> 提高代码复用性，安全性，隐藏实现的细节

    类的声明和类方法的定义：
        class <类名> {
            private：<私有成员函数/数据成员的声明>
            public：<公有成员函数/数据成员的声明>
        };
        <函数类型> <类名>::<成员函数名>(参数表){
            <函数体>
        }
    【成员函数又称“方法”，是类内部和外部程序的接口，通过类的实例化对象调用成员函数】
    【成员函数在类内部声明，外部定义】

    类的三大访问级别/访问控制属性：【也是继承的三种类型，此处不做详解】
        1.public ：需要被外界访问的成员【被实例化对象调用】
        2.private ：只能在当前类中访问的成员【只有类中成员可调用】
        3.protected ：只能在当前类和子类中访问的成员
    【注：类中数据类型无法直接访问，通过成员函数进行访问数据】
    【注：三者出现次序无关，可多次出现】
    【注：一个成员只能由一种访问属性】

对象的使用（即创建实例化对象）
        <类名> <实例化对象名>(传入类中的参数)
    创建了实例对象后，可通过实例对象调用成员函数，实现外部和类的交互
        <实例对象名>.<公有成员数据名>
        <实例对象名>.<公有成员函数名>(参数表)
    【注：成员可调用私有成员，但依然不可以实例对象给拿出来，即对外界不可见】

构造函数和析构函数：
    【构造函数】
    1.构造函数在public中，名字与类名相同，用于构造实例的类对象
    2.构造实例对象的任何初始化由构造函数自动完成
    3.构造函数可在构造实例对象时传入参数，赋值给private私有成员数据，供成员函数调用
    4.构造函数可在类中定义
    5.若无构造函数，编译器自动生成一个不带参数的缺省构造函数
        【此时创建对象，所有数据成员的值都初始化为空/0】
    6.可以是内联函数，也可以重载【初始化不同的类对象】
    【析构函数】
    1.释放一个实例对象，本身并不删除对象，而是系统放弃对象之前的清理工作【与构造相反】
    2.也属于成员函数，无参数无返回值，不可重载【即一个类只能由一个析构函数】
    3.使用析构函数：~ <类名>;     即释放该类
    4.系统也可自动调用，如函数/new动态申请，在结束时自动调用析构函数
    5.若无析构函数，编译器自动生成一个默认的析构函数，该析构函数为一个空函数，无作用
```

```c++
指针
    指针变量储存的是一个十六进制地址（32位整数），通过*对指针进行声明和访问【指针声明符/地址访问符】
指针类型：
    int *   char *   float *   double *   bool *
        - 可与整数进行【加减运算】，即求指针连续内存
        - 可指针之间进行【减法运算】，即求内存的相对距离
    void *:空类型指针，类型不确定，使用时必须强转类型【不可做算术运算】
    空指针:NULL,表示无效指针值，为0

  - 指向同一个数据的不同指针，地址值相同
  - 【同类型】的指针才可相互赋值（不同指针储存宽度不同）
  - 常量只能通过【强转类型】，以地址的形式赋值给指针，不能用&取地址
  - 内存线性存储，内存在前则地址小，地址+1则后退
  - 数组名本质为数组的首地址指针，可将数组名地址赋值给指针，不可将指针赋值给数组名【数组内存固定】

【注:当函数传入一个地址时，可在函数中对该地址的数据进行更改，该地址为形参，不改变实参】
```

```c++
有趣的一些指针：
    const与指针的结合：
        const int *p :【指向常量的指针】，const修饰的是指针指向的值 
                        ----- 不可修改指针指向的值，可改变指向地址
        int * const p :【常指针】，const修饰的是指针本身 
                        ----- 不可修改指向对象，可修改指向地址的数据
       const int * const p :【指向常量的常指针】，指针/数据都不可修改
    函数与指针的结合：
        int * fun() :指针函数，返回一个int *类型的指针
                【返回时不能返回局部变量的指针，若返回空指针则为函数运行失败】
        int (* fun)() :函数指针，此时fun为某一int类型函数的指针，* fun调用该函数
                【函数指针，即将函数调用口的功能赋值给一个相同类型、相同参数表的函数指针】
```

```c++
动态分配（C/C++）【存放在堆中，但凡申请则一定要手动释放】
    C语言：【以malloc.h为头文件】
        以malloc/free进行动态申请内存和释放【calloc，realloc】
        int *p = (int *)malloc(size)    --------->  以总字节数申请
                - size为所需申请的总内存大小（以字节为单位），返回为void类型指针
                - 需要将malloc进行强制转换为int */char */double *
                - 申请不成功返回为NULL
        free(*p)    手动释放申请p指针的内存
    C++：【不需要额外头文件】
        以new/delete进行动态申请内存和释放
        int *p = new int [长度]       --------->  以该类型的倍数申请
                - new int为new int[1]缩写
                - 此时p指针指向申请的连续地址的首地址
        delete p
                - 释放p所指向的【一个内存地址】
        delete []p
                - 释放p指针连续的【所有内存地址】

    注意事项：
        1.new申请的内存空间只允许使用一次delete，不可多次释放
        2.delete只可释放申请的内存，不可释放别的变量/常量

    关于malloc/free和new/delete的异同点：
        1.new/delete是关键字/操作符，可直接使用
          malloc/free为函数，存于malloc.h头文件中
        2.new返回定义的类型指针
          malloc返回void *指针
        3.new分配失败则报异常
          malloc分配失败返回NULL
        4.new/delete允许重载
          malloc/free不允许 
    （*）
        5.new面向对象申请空间内存
          malloc面向内存申请
        6.new：内部调用构造函数直接生成对象
          malloc：非操作符，不在编译器控制权限内   
```

```c++
链表问题 ---> 存储单元上非连续、非顺序

    以结构体为结点，同时储存数据和下一个节点指针，所形成的链状结构
    【头指针】-->【结点数据、结点指针】--> … --> 【结点数据、结点指针】--> NULL
    以动态申请结点内存，以指针连续指向为链条

链表类型：
    单向链表：单向，不可逆性
    双向链表：双向，头尾结点同时具有头指针和NULL，每个节点两个指针，可逆
    单向循环链表：单向循环，头指针指向某一个结点，以圆形循环指向，不存在尾结点和NULL指针
    双向循环链表：双向循环，头指针指向某一个结点，以圆形循环指向，不存在尾结点和NULL指针
                  每一个结点两个指针，可逆

    单向链表的数据操作：【单向循环如下，查询时结点指向查询起始结点为止】
        【传参可传数据也可传指针，但一定要确定头指针可用】
        1.查询：从头指针开始遍历指针，查询数据是否为被查询数据
        2.删除：从头指针开始遍历指针，先查询所需删除的结点位置
                同时保留前一个结点的指针，查询到之后前一个结点指针指向后一个结点
        3.插入：
                - 需要再申请一个【动态结点的空间内存】
                - 从头指针开始遍历指针，先查询所需插入在前的结点位置
                - 同时保留前一个结点的指针，查询到之后前一个结点指针指向插入结点
                - 插入节点指针指向被查询到的结点
                - 若查询不到则默认插入最后一个节点【包含空表】

    C语言：函数传入被操作数据/指针，同时【一定传入头指针】
    C++ ：可与C语言类似，可也建立一个【链表类】，头指针位于private，类函数可调用
            对链表类的操作函数，位于public，类似于C语言函数作用

    简单的双向链表操作：【单向循环如下，查询时结点指向查询起始结点为止】
        1.查询：可在单向基础上反方向查询
        2.删除：需要前后结点的各自一个指向被删结点的指针
                将前后结点的两个【反向且共同指向被删结点】的指针互指
        3.插入：在单向链表查询的基础上，同样需要得到前后结点的各自一个指向彼此的指针
                将两个指针同时指向插入的结点
                再将插入结点的两个指针指向前后结点【注意指针对应的前后顺序】


```

![CE19F45AF84C16C292FC240FBBFC595A](C:\Users\86180\Documents\Tencent%20Files\407981034\Image\C2C\CE19F45AF84C16C292FC240FBBFC595A.jpg)

```c++
C++程序结构
    作用域【不可改变】 ---> 即变量有效使用的【区域】
        1.函数原型作用域-----即形参名，包含数据类型，形参名可省略
        2.块/局部作用域------即函数内定义的局部变量，【函数结束则释放内存】
                上一层级不可调用下一层级【不可见】，下一层级可调用上一层级【作用域包含关系】
        3.文件作用域---------即【全局变量】
        4.可见性-------------即相同变量时，上一层级变量不可见，【就近原则】
【注：全局变量未赋值默认为0，局部变量未赋值为随机数】

    生存期【可改变】 ---> 即变量所占内存【持续时间】
        1.静态生存区----------即从创建开始一直到程序结束才释放内存
        2.自动生存区----------即创建后，根据局部作用域，函数结束自动释放内存
        3.动态生存区----------动态申请内存，手动进行结束释放

编程存储结构：【根据生存期进行分类存储】
    - 代码区：存储自己所写的代码和进行编译的二进制文件，不可修改，可执行
    - 数据/全局/静态存储区：存储生存期为静态生存期的数据/常量
            【const static define】三者仅改变生存期，【不改变作用域】
    - 栈：存储自动生存区的数据（包括函数），先进后出，用完释放内存
    - 堆：存储动态生存去的数据，手动申请内存，手动释放
【static声明的静态全局变量，在多文件情况下拒绝被其他文件调用，extern声明的全局变量为外部变量（默认）】

多文件结构：
    头文件（类声明文件）
        - 各种常量/宏定义/函数/自定义结构/类 的【声明】
        - 为防止预处理命令多次被编译，通常所需预处理命令全放入此处
        - 在头文件加入#pragma once防止多次编译
        - 通过#ifdef，#ifndef，#endif进行检测【条件编译】
    源文件1（类实现文件）
    源文件2
        - 各种类/函数/自定义结构 的【定义】
        - 默认为外部类型【extern】
    …
    主程序文件（类使用文件）
        - 以#include进行文件包含【双引号/尖括号】 ----> 当前目录查找，查询不到则查询系统目录
        - 可直接使用所定义的内容和已导入的头文件
        - 作为整个程序设计的主干，以一个功能一个源文件的形式

有趣的宏定义： 【比函数快，省内存，比conset慢，在嵌入式应用极多】
    #define ：经典定义宏，可定义常量/表达式/宏定义函数
                - 宏定义函数 ：#define <函数名>(参数表) (函数表达式【嵌入类型，注意括号】)
                - 函数名与参数表之间不可有空格
                - 参数表不具有数据类型
                - 注意传参后表达式的括号和【运算优先级】
                - 可用do { …函数体… } while（0）定义复杂的函数【换行以\进行】                
    #if/#elif/#endif ：条件编译，符合条件才进行编译
                - #endif任何条件编译必须有
                - #elif前必须有#if
    #ifdef/#ifndef/#endif ：保护头文件，判断宏名是否已被创建，避免多次编译出错
    #pragma ：#pragma once 与上一个作用相同
                - #pragma博大精深，有待发掘

好玩的常量：INT8/16/32/64_MAX/MIN ---> 求的1/2/4/8字节的最大值/最小值
                - INT8/16/32/64_MIN == (-INT8/16/32/64_MAX-1)
                - INT前加U表示unsigned，UINT8/16/32/64_MAX/MIN值 == 最大值-最小值 == 最大值*2+1

名称空间 ：为防止大项目名称相互冲突，将不同类型名称存储在不同名称空间【更改可见性】
    using namespace std ：即为使用std的名称空间 == std::cin/std::cout 【局部使用】
        - 单独调用                 <名称空间>::<使用名称>    std::cin
        - 单独打开使用名称空间     using std::cin            cin
        - 使用全部命名空间         using namespace std       cin
        - 名称空间也具有可见性：
                【即在下一层级使用的命名空间，上一层级不可见】
        - 可用namespace进行【同名/不同运算/参数表相同】的函数封装
                通过使用不同命名空间权限，使用不同的函数
        【注：区别于函数重载：内容不一定相同/函数名相同/参数表至少有一个不同
                   名称空间：内容一定不同/函数名相同/参数表相同】
        - namespace <名称空间名> { 该名称空间成员的声明 };

异常处理机制：try - throw - catch
        - try{ 检测语句 } ---> 对检测语句内进行保护和检测
        - throw(异常信息) ---> try若遇到异常，通过判断用throw将异常信息抛出，try结束运行
        - catch(参数类型 参数){ 对异常的处理语句 }
                         ---> catch语句可有多个，不同参数对应不同异常类型
                         ---> throw抛给catch进行接收，与catch参数进行匹配确定异常类型
```

```c
文件缓冲区：
        程序输入/输出 ---> 进入缓冲区 ---> 写入磁盘文件
        【存在多个缓冲区，每一个缓冲区512B】、

      全缓冲 ：【直接对磁盘读写】，每一个缓冲区需要填满才进行I/O操作
      行缓冲 ：【标准流输入/输出：stdin/stdout】，回车进行I/O操作
      不带缓冲 ：【标准流错误：stderr】，直接显示不进行缓冲

    清空缓冲区操作：【EOF，end of file，作为文件的结束标志】
        fflush() ：清空缓冲区    【不是C标准中的，部分编译系统不支持】
        fflush(stdin) ：清空标准输入缓冲区
        fflush(stdout) ：清空标准输出缓冲区
        getchar() ：清除缓冲区中的一个字符 【while(getchar!='\n') continue;循环清空缓冲区】
        setbuf() ：将stdin输入流转化为不带缓冲区 【通用性差，Linux不可用】
      【有关文件相关操作（非I/O流类），详情见C语言笔记（如果没有那就是我还没写）】
```

```c++
I/O流类库【数据以流的形式从一个对象流向另一个对象】
   （以面向对象的角度，以类的操作进行I/O操作）
        标准流对象：cin/cout【标准输入/输出】
                   cerr：标准错误输出，无缓冲之间输出
                   clog：标准错误输出，有缓冲，缓冲区满的时候直接输出
        标准流实现：<</>>

        cout输出类型控制：
                流控制符【cout<<控制符<<数据;】
                    - dec/hex/oct ：以十进制/十六进制/八进制输出
                    - setw(n) ：设置域宽【不截断】
                    - setfill(ch) ：以ch进行填充
                    - setprecision(n) ：浮点数小数位数为n
                流格式控制成员函数【cout.成员函数() cout<<数据;】
                    - .flags(ios::dec/hex/oct) ：以十进制/十六进制/八进制输出
                    - .width(n) ：设置域宽【不截断】
                    - .fill(ch) ：以ch进行填充
                    - .precision(n) ：浮点数小数位数为n
                                【后面一定要有cout.flags(ios::fixed);】
                【拓展】
                    - .ignore(n) ：忽略前n个字符
                    - 
        【注，两者控制都是一次性效力，再输出需要重新添加控制符】
        【注：两者都可叠buff，具有多种控制格式】

        cin输入类型控制：
                字符串输入：1.可直接输入无空格/回车的字符串
                            2.以cin.getline(str,n,ch)控制
                                - str为字符串首地址，n为录入长度，ch为结束条件，默认为\n
                                - 超出长度时，只读取【n-1】个字符
                                - ch不被录入字符串
                           3.以cin.get(str,n,ch)初步认为和getline使用上没区别


【下略】
串流类【头文件strstream】
        istrstream【串流类输入】
        ostrstream【串流类输出】

文件流类【头文件fstream】
        文件：文本文件【以ASCII/UTF-8存储】/二进制文件【音频/图片/可执行文件等二进制存储】【流式文件】
              普通文件/设备文件【与外部相连】
        ifstream【文件输入流】
        ofstream【文件输出流】
```









