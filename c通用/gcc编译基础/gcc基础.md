# gcc编译器

gcc（GNU Compiler Collection，GNU 编译器套件），是由 GNU 开发的编程语言编译器。gcc原本作为GNU操作系统的官方编译器，现已被大多数类Unix操作系统（如Linux、BSD、Mac OS X等）采纳为标准的编译器，gcc同样适用于微软的Windows。

gcc最初用于编译C语言，随着项目的发展gcc已经成为了能够编译C、C++、Java、Ada、fortran、Object C、Object C++、Go语言的编译器大家族。

编译命令格式：

gcc [-option1] ... <filename>
g++ [-option1] ... <filename>
1
2
命令、选项和源文件之间使用空格分隔
一行命令中可以有零个、一个或多个选项
文件名可以包含文件的绝对路径，也可以使用相对路径
如果命令中不包含输出可执行文件的文件名，可执行文件的文件名会自动生成一个默认名，Linux平台为a.out，Windows平台为a.exe
gcc、g++编译常用选项说明：

选项	含义
-o file	指定生成的输出文件名为file
-E	只进行预处理
-S(大写)	只进行预处理和编译
-c(小写)	只进行预处理、编译和汇编
C语言是不跨平台的，用Java用习惯的我突然回到C，有点不适应，用SpringBoot完成的Java项目，打成jar包，只要安装了Java的环境，哪个地方都能跑。

对于C来说Linux编译后的可执行程序只能在Linux运行，Windows编译后的程序只能在Windows下运行。64位的Linux编译后的程序只能在64位Linux下运行，32位Linux编译后的程序只能在32位的Linux运行。
————————————————

                        版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
原文链接：https://blog.csdn.net/qq_42322103/article/details/99071161/
