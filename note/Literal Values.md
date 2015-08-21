##Literal Values##
[本章的链接-Literal Value](http://www.asic-world.com/systemverilog/literal_values1.html#Integer_and_Logic_Literals)
###介绍###
SystemVerilog 在现存的Verilog基础上增加了一些新的数值常量，并且对一些常量进行了修改。

1. 时间量
2. 数组量
3. 结构体
4. 字符串的改进

###整型和逻辑常量-（Integer and logic Literals）###
按照2001年Verilog的规定，SystemVerilog的整型和逻辑常量可以是固也是定长度和非固定长度的。向任何变量赋常数值可以参考下列形式：

'0 : Set all bits to 0

'1: Set all bits to 1

'X or x : Set all bits to x

'Z or z : Set all bits to z

###实数常量-(Real Literals)###
定点格式和指数格式是实数的默认形式。我们能进行格式转换，将实数转换成短实数形式。下面列举了一些实数常量的例子：

* 3.14
* 2.0e16

**exmaple - real literal**
<code>

	module real_literals();
  	real a;
  	shortreal b;
  
  	initial begin 

    	$monitor("@%gns a=%e b=%e",$time,a,b);
    	$dumpfile("dump.vcd");
    	$dumpvars(1,real_literals);
    
    	a='0;
    	b=1.0e2;
    
    	#1 b=shortreal'(a);
    
    	#1 a=2e5;
    	#1 b=shortreal'(a);
    
    	#1 a=2.1e-2;
   	    #1 b=shortreal'(a);
    
    	#1 $finish;
  	end
	endmodule
</code>
simulator output:

- @0ns a=0.000000e+00 b=1.000000e+02
- @1ns a=0.000000e+00 b=0.000000e+00
- @2ns a=2.000000e+05 b=0.000000e+00
- @3ns a=2.000000e+05 b=2.000000e+05
- @4ns a=2.100000e-02 b=2.000000e+05

PS:实数的display格式为'%e',time常量的格式为'%g'.

###时间常量（Time Literals）###

时间常量是整数或固定长度实数格式，数值后面紧接着时间单位。根据当前的时间单位，时间常量作为实时时间量插入，并且根据当前时间精度循环。

- 1ns
- 1.4ps
- 0.01ns


**exmaple - time literal**
<code>

	module time_literals();
  
  	time a;
  	initial begin
    	$monitor("@%g a=%t",$time,a);
    
    	#1 a=1ns;
    	#1 a=0.2ns;
    	#1 a=300ps;
    
    	#1 $finish;
  	end
	endmodule

</code>

simulator output:

- @0 a=                   0
- @1 a=                 100
- @2 a=                  20
- @3 a=                  30

###字符串常量（String Literals）###
字符串常量带有引号，并且其有自己的数据形式。字符串里的字符必须处在一行内，新启一行必须在前面加上'\'。
特殊字符必须在前面加上'\'形成转义字符。字符常量还可以转换成压缩或非压缩数组。SystemVerilog增加了下列
特殊字符串常量。

- \v 垂直制表符
- \f 换页符（form feed）
- \a 警铃符
- \0x02 十六进制数据

**exmaple -string literal**
<code>

	module string_literals();
  
  	string a;
  
  	initial begin
    
    	$display("@%gns a=%s",$time,a);
    
    	a="Hello Deepak";
   	 	$display("@%gns a=%s",$time,a);
    
    	#1 a="Over writting old string";
    	$display("@%gns a=%s",$time,a);
    
    	#1 a="This is multi line comment and this is second line";
    	$display("@%gns a=%s",$time,a);
    
    	#1 $finish;
  	end
	endmodule

</code>

simulator output:

- @0ns a=
- @0ns a=Hello Deepak
- @1ns a=Over writting old string
- @2ns a=This is multi line comment and this is second line

###数组常量-（Array Literals）###
SystemVerilog除了复制操作符（'{}'），其在语法上与C语言相同。其嵌套的大括号跟随在维数后。

**exmaple -Array literals**
<code>

 	module array_literals ();
  
   		byte a [0:1][0:2] = '{'{0,1,2},'{3{8'hex5}}};

		initial begin
 	   		$display ("a [0][0] = %d", a[0][0]);
       		$display ("a [0][1] = %d", a[0][1]);
       		$display ("a [0][2] = %d", a[0][2]);
       		$display ("a [1][0] = %d", a[1][0]);
       		$display ("a [1][1] = %d", a[1][1]);
 	   		$display ("a [1][2] = %d", a[1][2]);
	   		#1  $finish;
 		end
    endmodule

</code>
simulator output:

- a [0][0] =           0
- a [0][1] =           1
- a [0][2] =           2
- a [1][0] =           5
- a [1][1] =           5
- a [1][2] =           5
###结构体-（Structure Literals）###
结构体在语法上与C语言相同。

**example - Structure Literals**

    typedef struct{
    	byte a;
      	reg b;
      	shortint unsigned c;
    }myStruct;
    
    module struct_literals();
      
      myStruct object='{10,0,100};
      myStruct objectArray [0:1]='{'{10,0,100},'{11,1,101}};
      
      initial begin
	    $display("a=%b b=%b c=%h",object.a,object.b,object.c);
	    object.a=15;
	    $display("a=%b b=%b c=%h",object.a,object.b,object.c);
	    object.c=16'hdead;
	    $display("a=%b b=%b c=%h",object.a,object.b,object.c.toupper);
	    
	    $display("Printing array of objects");
	    $display("a=%b b=%b c=%h",objectArray[0].a,objectArray[0].b,objectArray[0].c);
	    $display("a=%b b=%b c=%h",objectArray[1].a,objectArray[1].b,objectArray[1].c);
    
    	#1 $finish;
      end
    endmodule
simulator output:

- a=00001010 b=0 c=0064
- a=00001111 b=0 c=0064
- a=00001111 b=0 c=dead
- Printing array of objects
- a=00001010 b=0 c=0064
- a=00001011 b=1 c=0065

$finish called from file "testbench.sv", line 25.



