## 3.11 截断文件

使用系统调用 truncate()或 ftruncate()可将普通文件截断为指定字节长度，其函数原型如下所示：

#include <unistd.h>

#include <sys/types.h>

int truncate(const char \*path, off\_t length);

int ftruncate(int fd, off\_t length);

这两个函数的区别在于：ftruncate()使用文件描述符 fd 来指定目标文件，而 truncate()则直接使用文件路

径 path 来指定目标文件，其功能一样。

这两个函数都可以对文件进行截断操作，将文件截断为参数 length 指定的字节长度，什么是截断？如

果文件目前的大小大于参数 length 所指定的大小，则多余的数据将被丢失，类似于多余的部分被“砍”掉

了；如果文件目前的大小小于参数 length 所指定的大小，则将其进行扩展，对扩展部分进行读取将得到空字

节"\\0"。

使用 ftruncate()函数进行文件截断操作之前，必须调用 open()函数打开该文件得到文件描述符，并且必

须要具有可写权限，也就是调用 open()打开文件时需要指定 O\_WRONLY 或 O\_RDWR。

> ### 调用这两个函数并不会导致文件读写位置偏移量发生改变，所以截断之后一般需要重新设置文件当前的读写位置偏移量，以免由于之前所指向的位置已经不存在而发生错误（譬如文件长度变短了，文件当前所指向的读写位置已不存在）。

调用成功返回 0，失败将返回-1，并设置 errno 以指示错误原因。

使用示例

示例代码 3.11.1 演示了文件的截断操作，分别使用 ftruncate()和 truncate()将当前目录下的文件 file1 截

断为长度 0、将文件 file2 截断为长度 1024 个字节。

示例代码 3.11.1 文件截断操作

#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

#include <sys/types.h>

#include <sys/stat.h>

#include <fcntl.h>

int main(void)

{

int fd;

/\* 打开 file1 文件 \*/

if (0 > (fd = open("./file1", O\_RDWR))) {

perror("open error");

exit(-1);

}

/\* 使用 ftruncate 将 file1 文件截断为长度 0 字节 \*/

if (0 > ftruncate(fd, 0)) {

perror("ftruncate error");

exit(-1);

}

/\* 使用 truncate 将 file2 文件截断为长度 1024 字节 \*/

if (0 > truncate("./file2", 1024)) {

perror("truncate error");

exit(-1);

}

/\* 关闭 file1 退出程序 \*/

close(fd);

exit(0);

}

上述代码中，首先使用 open()函数打开文件 file1，得到文件描述符 fd，接着使用 ftruncate()系统调用将

文件截断为 0 长度，传入 file1 文件对应的文件描述符；接着调用 truncate()系统调用将文件 file2 截断为 1024

字节长度，传入 file2 文件的相对路径。

接下来进行测试，在当前目录下准备两个文件 file1 和 file2，如下所示：

图 3.11.1 准备 file1 文件和 file2 文件

可以看到 file1 和 file2 文件此时均为 592 字节大小，接下来运行测试代码：

图 3.11.2 测试结果

程序运行之后，file1 文件大小变成了 0，而 file2 文件大小变成了 1024 字节，与测试代码想要实现的功

能是一致的。
