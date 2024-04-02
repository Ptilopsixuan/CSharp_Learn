类型：预定义类、自定义类
    int: 32位 -2^31 ~ 2^31-1
自定义类：
	public class FirstClass:
	{
		int onePara;						//field			数据成员
		static twoPara						//field 		静态数据成员
		public FirstClass(int onePara)		//Constructor	函数成员
			{this.onePara = onePara} 	
		public int oneMethod(){return 0;}	//Method		函数成员
	}
实例化
	FirstClass firstCase = new FirstClass(0);
成员调用
	firstCase.onePara						//一般数据成员
	Firs.twoPara							//类的静态成员
转换：显式转换 implicit 、隐式转换 explicit
类型的一种分类：值类型、引用类型、泛型类型、指针类型

	值类型：		赋值时会在内存重新创建实例，更改只会更改自身变量。	不能为null
		数值类型：
			有符号整数: sbyte, short, int, long
			无符号整数: byte, ushort, uint, ulong
			实数: float, double, decimal
		bool
		char
	引用类型：	赋值仅会复制引用，更改会导致所有引用一起更改。		可为null，表示不指向任何对象
		string
		object
		
	数值后缀：
		float: 		f	常用
		double: 	d
		decimal:	m	常用
		uint: 		u
		long: 		l
		ulong: 		ul
	
	数值字面量：
		十六进制：前缀 0x
		int million = 1_000_000;
		double million = 1e06;	未指定情况下，含有. 与e 会被认为是double。
		
	数值转换：
		子集可向父级隐式转换，父级向子集只能显示转换。
		小数向整数转换会舍去小数点后数值，System.Convert有舍入方法。
		大整数转浮点会损失数值精度。
		所有整数类均为decimal类的子集。
	
	整数运算：
		整数除法会取floor。
		整数溢出会导致其在数组内循环:	int a = int.MinValue; a--; a == int.MaxValue; -> true
			防止溢出要使用checked:		int c = checked(a++); 
									checked{}				-> OverflowException
			或打开/checked+开关(Visual Studio中Advanced Build Settings)
			此时用unchecked 回避溢出报错。
		
	
	