Chisel中的基本的数据类型：
==

无符号整数
----

>1.U       
// decimal 1-bit lit from Scala Int.  
>"ha".U    
// hexadecimal 4-bit lit from string.  
>"o12".U   
// octal 4-bit lit from string.  
>"b1010".U   
// binary 4-bit lit from string.  
    
有符号整数
------

>5.S    
// signed decimal 4-bit lit from Scala Int.  
>-8.S   
// negative decimal 4-bit lit from Scala Int.  
>5.U    
// unsigned decimal 3-bit lit from Scala Int.

显式定义位宽
------

（对于常量，chisel会默认使用最小位宽来保存，有符号类型会包括一个符号比特，也可以使用显式定义来指定常量的位宽。）
>8.U(4.W)   
// 4-bit unsigned decimal, value 8.  
>-152.S(32.W)   
// 32-bit signed decimal, value -152.  

布尔数
-----

>true.B   
// Bool lits from Scala lits.  
>false.B
