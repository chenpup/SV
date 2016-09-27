##Data Type Part V##
[本章的链接-Data Type](http://www.asic-world.com/systemverilog/data_types5.html#User_defined_types)


###整数类型####
自定义数据类型与C语言类似。用户能够定义自己想要的数据类型，自定义的数据类型在使用前必须预先定义，只要通过typedef定义为一个空的类型。

**语法**

- typedef data_type type_identifier variable_dimension
- typedef interface_instance_identifier.type_identifier;
- typedef [enum |struct |union|class] type_identifier;

通常类型的内容在定义之前，用户自定义数据类型需要预先申明。下列是源自enum，struct，unition 和class的用户自定义数据类型。

- typedef enum type_declaration_identifier
- typedef struct type_declaration_identifier
- typedef union type_declaration_identifier
- typedef class type_decaration_identifier
- typedef type_declaration_identifier

**Example-typedef**
<code>

	typedef struct{
	  byte a;
	  reg b;
	  shortint unsigned c;
	}mystruct;
	
	module typedef_data();
	//full typedef here
	  typedef integer myinteger;
	//typedef declaration without type
	  typedef myinteger;
	
	  myinteger a=10;
	  mystruct object='{10,0,100};
	
	  initial begin
	    $display("a=%d",a);
	    $display("Displaying object");
	    $display("a=%b b=%b c=%h",object.a,object.b,object.c);
	  end
	endmodule

</code>

**output**

Compiler version J-2014.12-SP1-1; Runtime version J-2014.12-SP1-1;  Sep 27 01:10 2016

- a=         10
- Displaying object
- a=00001010 b=0 c=0064

 
