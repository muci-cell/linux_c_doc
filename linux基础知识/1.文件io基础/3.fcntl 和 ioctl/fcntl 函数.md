# fcntl 函数

fcntl()函数可以对一个已经打开的文件描述符执行一系列控制操作，譬如复制一个文件描述符（与 dup、

dup2 作用相同）、获取/设置文件描述符标志、获取/设置文件状态标志等，类似于一个

> ### 多功能文件描述符管理工具箱。

fcntl()函数原型如下所示（可通过"man 2 fcntl"命令查看）：

#include <unistd.h>

#include <fcntl.h>

int fcntl(int fd, int cmd, ... /\* arg \*/ )

函数参数和返回值含义如下：

fd：文件描述符。

cmd：操作命令。

此参数表示我们将要对 fd 进行什么操作，cmd 参数支持很多操作命令，

大家可以打开 man 手册查看到这些操作命令的详细介绍，

这些命令都是以 F\_XXX 开头的，譬如 F\_DUPFD、F\_GETFD、F\_SETFD 等，

> ### 不同的 cmd 具有不同的作用，cmd 操作命令大致可以分为以下 5 种功能：

1. ⚫ 复制文件描述符（cmd=F\_DUPFD 或 cmd=F\_DUPFD\_CLOEXEC）；
2. ⚫ 获取/设置文件描述符标志（cmd=F_GETFD 或 cmd=F_SETFD）；
3. ⚫ 获取/设置文件状态标志（cmd=F_GETFL 或 cmd=F_SETFL）；
4. ⚫ 获取/设置异步 IO 所有权（cmd=F_GETOWN 或 cmd=F_SETOWN）；
5. ⚫ 获取/设置记录锁（cmd=F_GETLK 或 cmd=F_SETLK）；

这里列举出来，并不需要全部学会每一个 cmd 的作用，因为有些内容并没有给大家提及到，譬如什么

异步 IO、锁之类的概念，在后面的学习过程中，当学习到相关知识内容的时候再给大家介绍。

…：fcntl 函数是一个可变参函数，第三个参数需要根据不同的 cmd 来传入对应的实参，配合 cmd 来使

用。

返回值：执行失败情况下，返回-1，并且会设置 errno；执行成功的情况下，其返回值与 cmd（操作命

令）有关，譬如 cmd=F\_DUPFD（复制文件描述符）将返回一个新的文件描述符、cmd=F\_GETFD（获取文

件描述符标志）将返回文件描述符标志、cmd=F\_GETFL（获取文件状态标志）将返回文件状态标志等。

fcntl 使用示例

## (1)复制文件描述符

前面给大家介绍了 dup 和 dup2，用于复制文件描述符，除此之外，我们还可以通过 fcntl 函数复制文件

描述符， 可用的 cmd 包 括 F\_DUPFD 和 F\_DUPFD\_CLOEXEC ， 这 里 就 只 介 绍 F\_DUPFD ，

F\_DUPFD\_CLOEXEC 暂时先不讲。

当 cmd=F\_DUPFD 时，它的作用会根据 fd 复制出一个新的文件描述符，此时需要传入第三个参数，第

> 三个参数用于指出新复制出的文件描述符是一个大于或等于该参数的可用文件描述符（没有使用的文件描

述符）；如果第三个参数等于一个已经存在的文件描述符，则取一个大于该参数的可用文件描述符。

测试代码如下所示：

示例代码 3.10.1 fcntl 复制文件描述符

#include <sys/types.h>

#include <sys/stat.h>

#include <fcntl.h>

#include <unistd.h>

#include <stdio.h>

#include <stdlib.h>

int main(void)

{

int fd1, fd2;

int ret;

/\* 打开文件 test\_file \*/

fd1 = open("./test\_file", O\_RDONLY);

if (-1 == fd1) {

perror("open error");

exit(-1);

}

/\* 使用 fcntl 函数复制一个文件描述符 \*/

fd2 = fcntl(fd1, F\_DUPFD, 0);

if (-1 == fd2) {

perror("fcntl error");

ret = -1;

goto err;

}

printf("fd1: %d\\nfd2: %d\\n", fd1, fd2);

ret = 0;

close(fd2);

err:

/\* 关闭文件 \*/

close(fd1);

exit(ret);

}

在当前目录下存在 test\_file 文件，上述代码会打开此文件，得到文件描述符 fd1，之后再使用 fcntl 函数

复制 fd1 得到新的文件描述符 fd2，并将 fd1 和 fd2 打印出来，接下来编译运行：

图 3.10.1 fcntl 复制文件描述符测试结果

可知复制得到的文件描述符是 7，因为在执行 fcntl 函数时，传入的第三个参数是 0，也就时指定复制得

到的新文件描述符必须要大于或等于 0，但是因为 0\~6 都已经被占用了，所以分配得到的 fd 就是 7；如果传

入的第三个参数是 100，那么 fd2 就会等于 100，大家可以自己动手测试。

## (2)获取/设置文件状态标志

cmd=F\_GETFL 可用于获取文件状态标志，cmd=F\_SETFL 可用于设置文件状态标志。cmd=F\_GETFL 时

不需要传入第三个参数，返回值成功表示获取到的文件状态标志；cmd=F\_SETFL 时，需要传入第三个参数，

此参数表示需要设置的文件状态标志。

这些标志指的就是我们在调用 open 函数时传入的 flags 标志，可以指定一个或多个（通过位或 | 运算

符组合），但是文件权限标志（O\_RDONLY、O\_WRONLY、O\_RDWR）以及文件创建标志（O\_CREAT、

O\_EXCL、O\_NOCTTY、O\_TRUNC）不能被设置、会被忽略；在 Linux 系统中，只有 O\_APPEND、O\_ASYNC、

O\_DIRECT、O\_NOATIME 以及 O\_NONBLOCK 这些标志可以被修改，这里面有些标志并没有给大家介绍

过，后面我们在用到的时候再给大家介绍。所以对于一个已经打开的文件描述符，可以通过这种方式添加或

移除标志。

测试代码如下：

示例代码 3.10.2 fcntl 读取/设置文件状态标志

#include <sys/types.h>

#include <sys/stat.h>

#include <fcntl.h>

#include <unistd.h>

#include <stdio.h>

#include <stdlib.h>

int main(void)

{

int fd;

int ret;

int flag;

/\* 打开文件 test\_file \*/

fd = open("./test\_file", O\_RDWR);

if (-1 == fd) {

perror("open error");

exit(-1);

}

/\* 获取文件状态标志 \*/

flag = fcntl(fd, F\_GETFL);

if (-1 == flag) {

perror("fcntl F\_GETFL error");

ret = -1;

goto err;

}

printf("flags: 0x%x\\n", flag);

/\* 设置文件状态标志,添加 O\_APPEND 标志 \*/

ret = fcntl(fd, F\_SETFL, flag | O\_APPEND);

if (-1 == ret) {

perror("fcntl F\_SETFL error");

goto err;

}

ret = 0;

err:

/\* 关闭文件 \*/

close(fd);

exit(ret);

}

上述代码会打开 test\_file 文件，得到文件描述符 fd，之后调用 fcntl(fd, F\_GETFL)来获取到当前文件状

态标志 flag，并将其打印来；接着调用 fcntl(fd, F\_SETFL, flag | O\_APPEND)设置文件状态标志，在原标志的

基础上添加 O\_APPEND 标志。接下来编译测试:

图 3.10.2 fcntl 测试结果 2

以上给大家介绍了 fcntl 函数的两种用法，除了这两种用法之外，还有其它多种不同的用法，这里暂时

先不介绍了，后面学习到相应知识点的时候再给大家讲解。
