##数据类型-Part I##
[本章的链接-Data Type](http://www.asic-world.com/systemverilog/data_types1.html)
###介绍###
SystemVerilog为了改进运行时simulator占用的内存，改进了现有的数据类型以及在增加了很多新的数据类型。SystemVerilog的数据主要体现在以下几个方面：

- shortint 和 longint 数据类型；
- shortreal 数据类型（real类型已经在verilog中定义过)；
- string,chandle以及class数据类型；
- logic,bit和byte数据类型；
- typedef（用户定义类型）；
- struct，union和class数据类型；
- void 数据类型；
- null 数据类型；
- arrays，queue，关联（associative）array,动态array.

<b>注意</b>：在使用用户自定义类型(typedef)之前，需要预先定义。

###整型数据类型###
整数数据类型可以被分为2-state类型和4-state类型。2-state的状态只有：0，1；4-state的状态有：0,1,X,Z.
仿真时2-state memory占用的内存只有4-state的一半，并且速度比4-state快。

2-state的整数数据类型有：

- shortint: 16-bit带符号整数；
- int:32-bit带符号整数；
- longint：64-bit带符号整数；
- byte：8-bit带符号整数，用来存储ASCII码字符；
- bit:自定义型向量(vector)类型。

4-state的整数数据类型有：

- logic：自定义型向量(vector)类型；
- reg:自定义型向量(vector)类型；
- wire:自定义型向量(vector)类型；
- integer:32-bit带符号整数；
- time:64-bit无符号整数；

整型类型可以是带符号或无符号的，其会直接影响到算术操作的结果。所以在申明需要进行算术运算的数据类型时需要特别注意。byte,shortint,int,interger和longint默认为带符号的，同时bit,reg,logic和wire默认是无符号类型的。

<b>注意</b>：reg和logic是完全相同的数据类型。为了避免与reg数据类型混淆，引入了logic数据类型。

**Example-整数数据类型**

    module data_types();
     
      bit   data_1bit;
      byte  data_8bit;
      shortint  data_16bit;
      int   data_32bit;
      longint   data_64bit;
      integer   data_integer;
      
      bit   unsigned data_1bit_unsigned;
      byte  unsigned data_8bit_unsigned;
      shortint  unsigned data_16bit_unsigned;
      int   unsigned data_32bit_unsigned;
      longint   unsigned data_64bit_unsigned;
      integer   unsigned data_integer_unsigned;
      
      initial begin
	     data_1bit   = {32{4'b1111}};
	     data_8bit   = {32{4'b1111}};
	     data_16bit  = {32{4'b1111}};
	     data_32bit  = {32{4'b1111}};
	     data_64bit  = {32{4'b1111}};
	     data_integer= {32{4'b1111}};
	     $display("data_1bit= %0d",data_1bit);
	     $display("data_8bit= %0d",data_8bit);
	     $display("data_16bit   = %0d",data_16bit);
	     $display("data_32bit   = %0d",data_32bit);
	     $display("data_64bit   = %0d",data_64bit);
	     $display("data_integer = %0d",data_integer);
	     data_1bit   = {32{4'bzx01}};
	     data_8bit   = {32{4'bzx01}};
	     data_16bit  = {32{4'bzx01}};
	     data_32bit  = {32{4'bzx01}};
	     data_64bit  = {32{4'bzx01}};
	     data_integer= {32{4'bzx01}};
	     $display("data_1bit= %b",data_1bit);
	     $display("data_8bit= %b",data_8bit);
	     $display("data_16bit   = %b",data_16bit);
	     $display("data_32bit   = %b",data_32bit);
	     $display("data_64bit   = %b",data_64bit);
	     $display("data_integer = %b",data_integer);
	     data_1bit_unsigned   = {32{4'b1111}};
	     data_8bit_unsigned   = {32{4'b1111}};
	     data_16bit_unsigned  = {32{4'b1111}};
	     data_32bit_unsigned  = {32{4'b1111}};
	     data_64bit_unsigned  = {32{4'b1111}};
	     data_integer_unsigned  = {32{4'b1111}};
	     $display("data_1bit_unsigned  = %d",data_1bit_unsigned);
	     $display("data_8bit_unsigned  = %d",data_8bit_unsigned);
	     $display("data_16bit_unsigned = %d",data_16bit_unsigned);
	     $display("data_32bit_unsigned = %d",data_32bit_unsigned);
	     $display("data_64bit_unsigned = %d",data_64bit_unsigned);
	     $display("data_integer_unsigned = %d",data_integer_unsigned);
	     data_1bit_unsigned   = {32{4'bzx01}};
	     data_8bit_unsigned   = {32{4'bzx01}};
	     data_16bit_unsigned  = {32{4'bzx01}};
	     data_32bit_unsigned  = {32{4'bzx01}};
	     data_64bit_unsigned  = {32{4'bzx01}};
	     data_integer_unsigned  = {32{4'bzx01}};
	     $display("data_1bit_unsigned  = %b",data_1bit_unsigned);
	     $display("data_8bit_unsigned  = %b",data_8bit_unsigned);
	     $display("data_16bit_unsigned = %b",data_16bit_unsigned);
	     $display("data_32bit_unsigned = %b",data_32bit_unsigned);
	     $display("data_64bit_unsigned = %b",data_64bit_unsigned);
	     $display("data_integer_unsigned = %b",data_integer_unsigned);
	     #1  $finish;
      end
      
    endmodule

simulator output:

- data_1bit    = 1
- data_8bit    = -1
- data_16bit   = -1
- data_32bit   = -1
- data_64bit   = -1
- data_integer = -1
- data_1bit    = 1
- data_8bit    = 00010001
- data_16bit   = 0001000100010001
- data_32bit   = 00010001000100010001000100010001
- data_64bit   = 0001000100010001000100010001000100010001000100010001000100010001
- data_integer = zx01zx01zx01zx01zx01zx01zx01zx01
- data\_1bit_unsigned  = 1
- data\_8bit_unsigned  = 255
- data\_16bit_unsigned = 65535
- data\_32bit_unsigned = 4294967295
- data\_64bit_unsigned = 18446744073709551615
- data\_integer_unsigned = 4294967295
- data\_1bit_unsigned  = 1
- data\_8bit_unsigned  = 00010001
- data\_16bit_unsigned = 0001000100010001
- data\_32bit_unsigned = 00010001000100010001000100010001
- data\_64bit_unsigned = 0001000100010001000100010001000100010001000100010001000100010001
- data\_integer_unsigned = zx01zx01zx01zx01zx01zx01zx01zx01

<b>注意</b>：对于带符号数来说，代码中data_8bit   = {32{4'b1111}}，是其补码。
-1的补码为：0000 0001 各位取反+1，即为1111 1111.

##数据类型-Part II##

###void 和null 数据类型###
SystemVerilog中void 和null数据类型与C语言是相同的，void用在没有返回值得函数(function)中。null用在将一个变量同空值做对比，例如将字符串同空字符串作对比。我们会在后面的class数据类型进行探讨。

###chandle数据类型###
chandle在使用直接编程接口（Direct Programming interface）中存放指针(pointer)。我们将在后面DPI章节进行探讨。




