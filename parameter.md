# 2. 栈和堆

栈：存放局部变量和常量。

堆：存放对象（如实例）。

## 2.1 默认值

引用类型:     null
数字与枚举类: 0
char:         '\0'
bool:         false

## 2.2 参数修饰 parameter -> argument

```text
修饰符    传递类型    必须赋值的变量
无        按值传递    传入
ref       按引用传递  传入
out       按引用传递  传出
```

### 2.2.1 按值传递

传递值类型时，创建一份参数值的副本。

```cs
static void f(int x) { x++; }
int a = 1; f(a); // a = 1
```

传递引用类型时，创建一份引用的副本。

### 2.2.2 ref 按引用传递

传入的是对象本身，必须在传入前赋值。<font color = red>声明与调用</font>时均需带有ref

```cs
static void f(ref int x) { x++; }
int a = 1; f(ref a); // a = 2
```

### 2.2.3 out 按引用传递

仅必须在函数结束前复制，其余同ref。本质上是将为该对象起一个昵称，传入函数并运算。

_: 丢弃符号，不建议用作变量名称。

```cs
Method (out _ ); //this parameter will be discarded.
```

### 2.2.4 params

只能修饰方法的最后一个参数，且必须是数组。

```cs
static int Sum (params int[] a) 
{
    int sum; 
    foreach (int b in a) { sun += b;}
    return sum;
}
int totle = Sum(0, 1, 2, 3, 4); //totle = 10
int totle_2 = Sum(new int[] {0, 1, 2, 3, 4});//也可无视params直接传入数组参数。
```

### 2.2.5 可选参数

在声明方法之时，若给予默认值，则调用时可不提供传入参数。

```cs
void F (int x = 1) { print(x); }
F()  // 1
F(1) // 等效于此
```

params与ref/ out 不共存。

### 2.2.6 声明时的参数顺序

```cs
void Method (int a, int b = 1, params int[] c){}
```

### 2.2.7 : 命名参数

```cs
void M (int x, int y) {print(x + " " + y);}
M(x: 1, y: 2) // 1 2
M(y: 2, x: 1) // 1 2
M(1, y: 2)     // 1 2
M(x: 1, 2)     // Error, 按位置的参数必须在命名参数之前

int a = 0;
M(y: a++, x: a--) //0 1
```

命名参数常与可选参数(2.2.5)混合使用。

