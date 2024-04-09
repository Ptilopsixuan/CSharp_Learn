# 1. 类型基础

分类一：预定义类、自定义类

分类二：值类型、引用类型、泛型类型、指针类型

## 1.1 自定义类

```csharp
 public class FirstClass:
 {
    int onePara;      //field   数据成员
    static twoPara    //field   静态数据成员
    public FirstClass(int onePara) {this.onePara = onePara}  //Constructor 函数成员
    public int oneMethod(){return 0;} //Method  函数成员
 }
 ```

### 1.1.1 实例化

```csharp
FirstClass firstCase = new FirstClass(0);
```

### 1.1.2 成员调用

```csharp
firstCase.onePara  //一般数据成员
Firs.twoPara       //类的静态成员
```

### 1.1.3 转换

显式转换 implicit 、隐式转换 explicit

## 1.2 类型的第二种分类

### 1.2.1 值类型

赋值时会在内存重新创建实例，更改只会更改自身变量。且不能为null。

```text
数值：
    有符号整数: sbyte(8bit) short(16bit)  int(32bit)  long(64bit)
    无符号整数: byte(8bit)  ushort(16bit) uint(32bit) ulong(64bit)
    实数: float(*single)(32bit)   double(64bit)    decimal(128bit)
bool
char
```

### 1.2.2 引用类型

赋值仅会复制引用，更改会导致所有引用一起更改。可为null，表示不指向任何对象。

```text
string
object
```

## 1.3 预定义类型

### 1.3.1 数值类型

#### 1.3.1.1 数值后缀

```text
float:   f 常用
double:  d
decimal: m 常用
uint:    u
long:    l
ulong:   ul
```

#### 1.3.1.2 数值字面量

```text
十六进制：前缀 0x
int million = 1_000_000; 可在数字间插入_以便于阅读。
double million = 1e06; 未指定情况下，含有. 与e 会被认为是double。
```

#### 1.3.1.3 数值转换

子集可向父级隐式转换，父级向子集只能显示转换。

小数向整数转换会舍<font color = red>去</font>小数点后数值，System.Convert有舍入方法。

大整数转浮点会损失数值精度。

所有整数类均为decimal类的子集。

#### 1.3.1.4 整数运算

##### 整数除法会取floor

##### 整数溢出会导致其在数组内循环

```csharp
int a = int.MaxValue; a++; a == int.MinValue; // true
```

防止溢出要使用checked:  

```cs
int c = checked(a++); //or
checked{ c = a + 1; } // OverflowException
```

或打开/checked+开关(Visual Studio中Advanced Build Settings)

此时用unchecked 回避溢出报错。

##### byte sbyte(8bit) short ushort(16bit) 无法算术运算，运算时会隐式转为int，故无法将运算结果直接赋予自身类型

##### 位运算符

```text
~  按位取反
&  按位与
|  按位或
^  按位异或
<< 按位左移
>> 按位右移
```

#### 1.3.1.5 浮点数运算

```cs
//特殊常量: NaN, Infinity, NegativeInfinity, -0.0
0.0/0.0 // NaN
Infinity - Infinity // NaN
NaN != NaN // true 
//如需判断NaN需调用 
float.IsNaN(), double.IsNaN(), object.Equals(,)
//其他常量: MaxValue, MinValue, Epsilon
//double 与 decimal
double //基数为2， 范围大，速度快，有特殊值  更适用于科学计算
decimal//基数为10，可以精确表示诸如0.1的数值 更适用于金融计算
```

### 1.3.2 bool类型运算

```cs
&& // 与 短路运算 避免NullReferenceException 
    if (a != null && a.length > 0)
|| // 或
！ // 非
?  // 三元运算符 
    q ? a : b // q为真时返回a，为假时返回b。
```

### 1.3.3 字符&字符串

#### 转义字符

```cs
'\'' // '
'\"' // "
'\\' // \
'\o' // null
'\a' // 警告
'\b' // 退格
'\f' // 走纸
'\n' // 换行
'\r' // 回车
'\t' // 水平制表符
'\v' // 垂直制表符
```

#### @

```cs
string path = @"C:\MyDoc\CS"  // 变为原意字符串字面量，将不转义“”内\，且可换行，
string a = @"""hello world""" //此情况字面量内的“”需用两个““””。
```

#### $

若与@共用，必须写作$@

```cs
int x = 10;
string joke = $"世界上只有{x}种人。"
```

### 1.3.4 数组[]

```cs
int[] a = new int[5];
int[] b = new int[] {1, 2, 3, 4, 5};
int[] b = {1, 2, 3, 4, 5};
```

数组本身时<font color =red>引用类型</font>，但其内部的元素是值类型亦或引用类型不会改变。
若数组内部为<font color =red>引用类型</font>，则需<font color =red>显示实例化每一个</font>元素。

```cs
int[] a = new int[5]; int x = a[1];          // x = 0
string[] b = new string[5]; string y = b[1]; // NullReferenceException
int[] a = null                               //Legal
```

#### IndexOutOfRangeException

### 1.3.5 多维数组

#### 1.3.5.1 矩形数组

```cs
int[,] matrix_a = new int[3,3];
int[,] matrix_b = new int[,] // new int[,] 可省去
{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

#### 1.3.5.2 锯齿数组

```cs
int[][] matrix_c = new int[3][];
int[][] matrix_d = new int[][]// new int[][] 可省去
{
    new int[] {1, 2},
    new int[] {3, 4, 5},
    new int[] {6, 7, 8, 9}
}
```

### 1.3.6 var: 让程序自行判断类型

```cs
var i = 3;
var s = "";
var m = new int[,];
```
