##Literal Values##
[本章的链接-Literal Value](http://www.asic-world.com/systemverilog/literal_values1.html#Integer_and_Logic_Literals)

###介绍###
SystemVerilog 在现存的Verilog基础上增加了一些新的数值常量，并且对一些常量进行了修改。

1. 时间量
2. 数组量
3. 结构体
4. 字符串的改进

###整型和逻辑常量###
按照2001年Verilog的规定，SystemVerilog的整型和逻辑常量可以是固也是定长度和非固定长度的。向任何变量赋常数值可以参考下列形式：

'0 : Set all bits to 0

'1: Set all bits to 1

'X or x : Set all bits to x

'Z or z : Set all bits to z

###实数常量###
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


**exmaple - real literal**
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