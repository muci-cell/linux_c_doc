当程序在执行某个函数出错的时候，如果此函数执行失败会导致后面的步骤不能在进行下去时，应该在

出错时终止程序运行，不应该让程序继续运行下去，那么如何退出程序、终止程序运行呢？有过编程经验的

读者都知道使用 return，一般原则程序执行正常退出 return 0，而执行函数出错退出 return -1，前面我们所编

写的示例代码也是如此。

在 Linux 系统下，进程（程序）退出可以分为正常退出和异常退出，注意这里说的异常并不是执行函数

出现了错误这种情况，异常往往更多的是一种不可预料的系统异常，可能是执行了某个函数时发生的、也有

可能是收到了某种信号等，这里我们只讨论正常退出的情况。

在 Linux 系统下，进程正常退出除了可以使用 return 之外，还可以使用 exit()、\_exit()以及\_Exit()，下面

我们分别介绍。原子哥在线教学：www.yuanzige.com 论坛：http://www.openedv.com/forum.php

67

I.MX6U

嵌入式 Linux C 应用编程指南

\_exit()和\_Exit()函数

main 函数中使用 return 后返回，return 执行后把控制权交给调用函数，结束该进程。调用\_exit()函数会

清除其使用的内存空间，并销毁其在内核中的各种数据结构，关闭进程的所有文件描述符，并结束进程、将

控制权交给操作系统。\_exit()函数原型如下所示：

#include <unistd.h>

void \_exit(int status);

调用函数需要传入 status 状态标志，0 表示正常结束、若为其它值则表示程序执行过程中检测到有错误

发生。使用示例如下：

示例代码 3.3.1 \_exit()使用示例

#include <sys/types.h>

#include <sys/stat.h>

#include <fcntl.h>

#include <unistd.h>

#include <stdio.h>

int main(void)

{

int fd;

/\* 打开文件 \*/

fd = open("./test\_file", O\_RDONLY);

if (-1 == fd) {

perror("open error");

\_exit(-1);

}

close(fd);

\_exit(0);

}

用法很简单，大家可以自行测试！

\_Exit()函数原型如下所示：

#include <stdlib.h>

void \_Exit(int status);

\_exit()和\_Exit()两者等价，用法作用是一样的，这里就不再讲了，需要注意的是这 2 个函数都是系统调

用。

exit()函数

exit()函数\_exit()函数都是用来终止进程的，exit()是一个标准 C 库函数，而\_exit()和\_Exit()是系统调用。

执行 exit()会执行一些清理工作，最后调用\_exit()函数。exit()函数原型如下：

#include <stdlib.h>原子哥在线教学：www.yuanzige.com 论坛：http://www.openedv.com/forum.php

68

I.MX6U

嵌入式 Linux C 应用编程指南

void exit(int status);

该函数是一个标准 C 库函数，使用该函数需要包含头文件<stdlib.h>，该函数的用法和\_exit()/\_Exit()是

一样的，这里就不再多说了。

本小节就给大家介绍了 3 中终止进程的方法：

⚫ main 函数中运行 return；

⚫ 调用 Linux 系统调用\_exit()或\_Exit()；

⚫ 调用 C 标准库函数 exit()。

不管你用哪一种都可以结束进程，但还是推荐大家使用 exit()，其实关于 return、exit、\_exit/\_Exit()之间

的区别笔者在上面只是给大家简单地描述了一下，甚至不太确定我的描述是否正确，因为笔者并不太多去

关心其间的差异，对这些概念的描述会比较模糊、笼统，如果大家看不明白可以自己百度搜索相关的内容，

当然对于初学者来说，不太建议大家去查找这些东西，至少对你现阶段来说，意义不是很大。
