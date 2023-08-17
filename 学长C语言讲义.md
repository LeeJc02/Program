## 01 数据类型

### 1 数据类型都有什么？

- 数据类型一共有这四种：基本类型、构造类型、指针类型、空类型void

- 整型和字符型又可以分为有符号（signed）和无符号（unsigned）
  
  在c语言中，默认的就是有符号的数据类型，signed是可以被省略的
  
  想要让我们的int等数据类型变为无符号整型，需要在前面加上关键字——unsigned
  
  ```c
  unsigned int a;
  ```
  
  有两个问题：
  
  有符号和无符号有什么区别吗？
  
  有符号和无符号的区别：就是在于最高位是否为符号位，
  
  signed：有符号整型最高位看作符号位
  
  unsigned：无符号整型最高位看作数值位
  
  为什么char类型也要和整型一样，分为有符号和无符号的？
  
  char类型本质上在内存中存储的就是整数，在输出的时候，我们输出的就是char类型对应的Unicode码
  
  ```c
  #include<bits/stdc++.h>
  int main(){
      char ch='a';
      printf("%c\n",ch);// 取字符
      printf("%i",ch);//取整型
      return 0;
  }
  ```

- 浮点型使用陷阱(比较2.7和8.1)
  
  ```c
  #include<bits/stdc++.h>
  #include<limits.h>
  #include<math.h>
  int main(){
      double num1=2.7;
      double num2=8.1/3;
      // 错误的写法
  //    if(num1==num2){
  //        printf("equal");
  //    } else {
  //        printf("not equal");
  //    }
      if(abs(num1-num2)<0.001){
          printf("equal");
      } else{
          printf("not equal");
      }
  }
  ```

### 2 为什么会有数据类型？

因为每种数据类型所占不同大小的内存，各种数据类型所能表示的数据范围也不相同

当编译器知道它所要处理的数据的类型之后,能够降低存储空间总量，并且能提高访问速度

- 以下为一些数据类型的存储大小和值范围
  
  ![img](assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FhOTg4NjU2NDY=,size_16,color_FFFFFF,t_70-16665171876753.png)

- sizeof方法：返回一个变量或类型的大小，以字节为单位

### 3 数据类型之间的转换

数据类型转换主要有两种：自动类型转换、强制类型转换

- 自动类型转换
  
  自动类型转换就是编译器默默地、隐式地、偷偷地进行的数据类型转换，这种转换不需要程序员干预，会自动发生。
  
  遵循以下规则：**精度小的类型自动转换为精度大的数据类型**，以保证数据不失真或者精度不降低
  
  ![image-20221023172728021](assets/image-20221023172728021.png)
  
  注意和细节：
  
  有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算。

- 强制类型转换
  
  当进行**数据从大到小**的转换时，就需要使用强制类型转换
  
  格式：
  
  ```c
  (type_name) expression
  ```
  
  以下为一些例子：
  
  ```c
  (float) a;  //将变量 a 转换为 float 类型
  (int)(x+y);  //把表达式 x+y 的结果转换为 int 整型
  (float) 100;  //将数值 100（默认为int类型）转换为 float 类型
  ```

## 02 函数

### 1 函数是什么

函数是一组一起执行一个任务的语句。每个 C 程序都至少有一个函数，即主函数 **main()** ，所有简单的程序都可以定义其他额外的函数。

当然了，函数在不同的语言中有不同的名字，比如方法、子例程或程序等

### 2 定义函数

```c
return_type function_name( parameter list )
{
   body of the function
}
```

在 C 语言中，函数由一个函数头和一个函数主体组成。下面列出一个函数的所有组成部分：

- **返回类型：**一个函数可以返回一个值。**return_type** 是函数返回的值的数据类型。有些函数执行所需的操作而不返回值，在这种情况下，return_type 是关键字 **void**。
- **函数名称：**这是函数的实际名称。函数名和参数列表一起构成了函数签名。
- **参数：**参数就像是占位符。当函数被调用时，您向参数传递一个值，这个值被称为实际参数。参数列表包括函数参数的类型、顺序、数量。参数是可选的，也就是说，函数可能不包含参数。
- **函数主体：**函数主体包含一组定义函数执行任务的语句。

具体实现

```c
/* 函数返回两个数中较大的那个数 */
int max(int num1, int num2) 
{
   /* 局部变量声明 */
   int result;

   if (num1 > num2) {
      result = num1;
   } else {
      result = num2;
   }
   return result; 
}
```

### 3 函数的声明

函数**声明**会告诉编译器函数名称及如何调用函数。

```c
return_type function_name( parameter list );
```

比方说：

```c
int max(int num1, int num2);
```

### 4 调用函数

```c
#include <stdio.h>
int max(int num1, int num2);
int main ()
{
   int a = 100;
   int b = 200;
   int ret;
   ret = max(a, b);
   printf( "Max value is : %d\n", ret );
   return 0;
}
int max(int num1, int num2) 
{
   int result;
   if (num1 > num2)
      result = num1;
   else
      result = num2;
   return result; 
}
```

### 5 函数参数

主要有值传递和引用传递

1. 值传递
   
   该方法把参数的实际值复制给函数的形式参数。在这种情况下，修改函数内的形式参数不会影响实际参数。

2. 引用传递
   
    通过指针传递方式，形参为指向实参地址的指针，当对形参的指向操作时，就相当于对实参本身进行的操作。

3. 比较
   
   ```c
   #include <stdio.h>
   void swap(int a,int b){
       int temp=a;
       a=b;
       b=temp;
   }
   void swap1(int &a,int &b){
       int temp=a;
       a=b;
       b=temp;
   }
   int main ()
   {
       int a = 100;
       int b = 200;
       swap(a,b);
       //swap1(a,b);
       printf("%d ",a);
       printf("%d",b);
       return 0;
   }
   ```

## 03 数组

### 1 数组定义

数组是有限的元素序列。所有的数组都是由连续的内存位置而组成的。最低的地址对应第一个元素，最高的地址对应最后一个元素。

数组中的特定元素可以通过索引访问，第一个索引值为 0。

我们可以看一下数组在内存中的存储。

### 2 声明数组

```c
type arrayName [ arraySize ];

int arr[10];
```

注意：arraySize必须是一个大于零的整数常量，**type** 可以是任意有效的 C 数据类型。

### 3 初始化数组

主要有三种形式：

1. ```c
   double balance[5] = {1000.0, 2.0, 3.4, 7.0, 50.0};
   ```

2. ```c
   double balance[] = {1000.0, 2.0, 3.4, 7.0, 50.0};
   // 此时，数组的大小则为初始化时元素的个数
   ```

3. ```c
   balance[4] = 50.0;
   // 把数组中第五个元素的值赋为 50.0
   ```

注意数组的下标是从0开始的，第一个元素的索引值为 **0**，第九个元素 的索引值为 **8**。

### 4 遍历数组

数组的输入和输出大都是通过循环来实现的。

实例：

```c
#include <stdio.h>
int main ()
{
    int n;//定义数组长度
    printf("请输入数组的长度：\n");
    scanf("%d",&n);//输入数组长度
    int a[n-1];//定义数组a
    printf("本次您总共输入了%d个元素\n",n);
    for(int i=0;i<n;i++)
    {
        printf("请输入第%d个元素：\n",i+1);
        scanf("%d",&a[i]);
    }
    printf("最终输出结果为：");
    for(int i=0;i<n;i++)
    {
        printf("%d ",a[i]);
    }
}
```

### 5 二维数组

#### 5.1二维数组的定义

二维数组的定义一般形式为：

```c
类型说明符 数组名[常量表达式][常量表达式]
```

比方说

```c
int a[3][4];
```

这个的意思就是定义了一个3行4列总共有12个元素的数组a。

#### 5.2二维数组的初始化

定义一个二维数组

```c
int a[5][4];
```

1. 分行给二维数组赋值
   
   ```c
   int a[3][4] = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}};
   ```

2. 按照数组排序对各元素赋值
   
   ```c
   int a[3][4] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
   ```

3. 对部分元素进行赋值
   
   ```c
   int a[3][4] = {{1, 2}, {5}, {9}};
   ```

#### 5.3 二维数组在内存中的存储

#### 5.4 二维数组遍历

```c
#include <stdio.h>
int main() {
    int  row, col; // 行、列
    printf("请输入二维数组的行和列\n");
    scanf("%d", &row);
    scanf("%d", &col);
    int a[row][col];
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col ; j++) {
            scanf("%d", &a[i][j]);
        }
    }
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col ; j++) {
            printf("%d", a[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

# 

markdown使用：这个一定要学一学

[ProcessOn思维导图、流程图-思维导图模板_思维导图软件免费下载_在线作图协作工具](https://www.processon.com/?utm_source=itab1)

clion：可以去玩一玩
