在 C 语言中，整型 `int` 是最常用的整数类型，用来表示整数。以下是整型变量的定义、输出格式以及输入的基本方法。

### 整型变量定义

```c
int a;       // 定义一个整型变量 a
int b = 10;  // 定义一个整型变量 b，并初始化为 10
```

### 整型变量的输出格式

可以使用不同的格式控制符来输出整型变量的值，以不同的进制格式显示。以下是常用的整型输出格式控制符：


| 打印格式 | 含义                                   | 示例代码             | 示例输出               |
| -------- | -------------------------------------- | -------------------- | ---------------------- |
| `%d`     | 输出一个有符号的 10 进制`int` 类型     | `printf("%d\n", a);` | `123`（正负视值而定）  |
| `%o`     | 输出一个 8 进制的`int` 类型            | `printf("%o\n", a);` | `173`（八进制）        |
| `%x`     | 输出一个 16 进制的`int` 类型，小写字母 | `printf("%x\n", a);` | `7b`                   |
| `%X`     | 输出一个 16 进制的`int` 类型，大写字母 | `printf("%X\n", a);` | `7B`                   |
| `%u`     | 输出一个无符号的 10 进制`int` 类型     | `printf("%u\n", a);` | `4294967163`（无符号） |

### 示例代码（输出不同进制表示的整型变量）

```c
#include <stdio.h>

int main() {
    int a = 123;
    printf("有符号 10 进制: %d\n", a);     // 输出：123
    printf("8 进制: %o\n", a);             // 输出：173
    printf("16 进制（小写）: %x\n", a);     // 输出：7b
    printf("16 进制（大写）: %X\n", a);     // 输出：7B
    printf("无符号 10 进制: %u\n", a);     // 输出：123
    return 0;
}
```

### 整型变量的输入

使用 `scanf` 函数来输入整型变量的值：

```c
#include <stdio.h>

int main() {
    int a;
    printf("请输入 a 的值：");

    // %d 表示读取一个有符号的 10 进制整数
    scanf("%d", &a);

    printf("a = %d\n", a); // 输出输入的整数值
    return 0;
}
```

**注意事项**：

- `scanf` 中 `%d` 表示输入一个 10 进制有符号整数；输入时不需要包含进制前缀。
- 输入变量时要使用地址符 `&`，如 `&a`。

### 整理总结


| 项目         | 内容                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------- |
| 变量定义     | `int a;` 或 `int b = 10;`                                                                         |
| 常用输出格式 | `%d`（10 进制）、`%o`（8 进制）、`%x`（16 进制小写）、`%X`（16 进制大写）、`%u`（无符号 10 进制） |
| 输入格式     | `scanf("%d", &a);`                                                                                |

通过这些方式，可以灵活地定义、输入和输出整型变量，并在不同进制之间进行转换和显示。
