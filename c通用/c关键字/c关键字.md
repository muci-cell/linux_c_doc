以下是整理后的表格，包括每个关键字的示例：


| 分类                     | 名称         1 | 描述                                                               | 示例                                                               1 |
| ------------------------ | -------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| **基本数据类型** (5个)   | `void`               | 声明函数无返回值或无参数，声明无类型指针，显式丢弃运算结果。       | `void func(void);`                                                                                   |
|                          | `char`               | 字符型数据类型。                                                   | `char letter = 'A';`                                                                                 |
|                          | `int`                | 整型数据，通常为编译器指定的机器字长。                             | `int number = 10;`                                                                                   |
|                          | `float`              | 单精度浮点型数据，保存小数点后6位。                                | `float value = 3.14f;`                                                                               |
|                          | `double`             | 双精度浮点型数据，保存小数点后15/16位。                            | `double preciseValue = 3.141592653589793;`                                                           |
| **类型修饰关键字** (4个) | `short`              | 修饰`int`，短整型数据，可省略被修饰的`int`。                       | `short num = 32767;`                                                                                 |
|                          | `long`               | 修饰`int`，长整型数据，可省略被修饰的`int`。                       | `long bigNum = 123456789L;`                                                                          |
|                          | `signed`             | 修饰整型数据，有符号数据类型。                                     | `signed int num = -123;`                                                                             |
|                          | `unsigned`           | 修饰整型数据，无符号数据类型。                                     | `unsigned int num = 123U;`                                                                           |
| **复杂类型关键字** (5个) | `struct`             | 结构体声明。                                                       | `struct Point { int x; int y; };`                                                                    |
|                          | `union`              | 共用体声明。                                                       | `union Data { int i; float f; };`                                                                    |
|                          | `enum`               | 枚举声明。                                                         | `enum Day { MON, TUE, WED };`                                                                        |
|                          | `typedef`            | 声明类型别名。                                                     | `typedef unsigned int uint;`                                                                         |
|                          | `sizeof`             | 获取特定类型或变量的大小。                                         | `size_t size = sizeof(int);`                                                                         |
| **存储级别关键字** (6个) | `auto`               | 指定为自动变量，编译器自动分配和释放，通常在栈上分配。             | `auto int var = 5;`                                                                                  |
|                          | `static`             | 静态变量，分配在静态变量区；修饰函数时，指定函数作用域为文件内部。 | `static int count = 0;`                                                                              |
|                          | `register`           | 建议编译器将变量存储在寄存器中；也可修饰函数形参。                 | `register int i = 0;`                                                                                |
|                          | `extern`             | 指定变量为外部变量，通常在其他文件中定义。                         | `extern int sharedVar;`                                                                              |
|                          | `const`              | 指定变量不可被当前线程/进程改变。                                  | `const int constant = 100;`                                                                          |
|                          | `volatile`           | 指定变量可能会被其他进程/线程改变，强制编译器每次从内存中读取。    | `volatile int flag = 0;`                                                                             |
| **跳转结构** (4个)       | `return`             | 在函数体中使用，返回特定值（或`void`值）。                         | `return 0;`                                                                                          |
|                          | `continue`           | 结束当前循环，开始下一轮循环。                                     | `continue;`                                                                                          |
|                          | `break`              | 跳出当前循环或`switch`结构。                                       | `break;`                                                                                             |
|                          | `goto`               | 无条件跳转语句。                                                   | `goto label;`                                                                                        |
| **分支结构** (5个)       | `if`                 | 条件语句。                                                         | `if (x > 0) { /* ... */ }`                                                                           |
|                          | `else`               | 条件语句否定分支（与`if`连用）。                                   | `if (x > 0) { /* ... */ } else { /* ... */ }`                                                        |
|                          | `switch`             | 多重分支语句。                                                     | `switch (x) { case 1: /* ... */; }`                                                                  |
|                          | `case`               | `switch`语句中的分支标记。                                         | `case 1: /* ... */;`                                                                                 |
|                          | `default`            | `switch`语句中的默认分支。                                         | `default: /* ... */;`                                                                                |
| **循环结构** (3个)       | `for`                | `for`循环结构。                                                    | `for (int i = 0; i < 10; i++) { /* ... */ }`                                                         |
|                          | `do`                 | `do`循环结构。                                                     | `do { /* ... */ } while (condition);`                                                                |
|                          | `while`              | `while`循环结构。                                                  | `while (condition) { /* ... */ }`                                                                    |

**数据类型的作用**：编译器利用数据类型来确定对象（变量）需要分配的内存空间大小。
