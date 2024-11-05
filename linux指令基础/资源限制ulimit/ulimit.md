以下是 `ulimit` 指令文档的翻译：(仅为临时修改)

---

### ulimit: `ulimit [-SHabcdefiklmnpqrstuvxPRT] [limit]`

**修改 shell 资源限制。**

在允许此类控制的系统上，`ulimit` 可控制 shell 和它创建的进程可以使用的系统资源。

**选项：**

- **-S**：使用“软”资源限制
- **-H**：使用“硬”资源限制
- **-a**：报告所有当前限制
- **-b**：套接字缓冲区大小
- **-c**：创建的核心转储文件的最大大小
- **-d**：进程数据段的最大大小
- **-e**：最大调度优先级（nice 值）
- **-f**：shell 及其子进程写入的文件的最大大小
- **-i**：挂起信号的最大数量
- **-k**：为该进程分配的 kqueues 的最大数量
- **-l**：进程可以锁定进内存的最大大小
- **-m**：最大驻留集大小
- **-n**：最大打开文件描述符数量
- **-p**：管道缓冲区大小
- **-q**：POSIX 消息队列的最大字节数
- **-r**：实时调度的最大优先级
- **-s**：最大栈大小
- **-t**：最大 CPU 时间（秒为单位）
- **-u**：最大用户进程数
- **-v**：虚拟内存的大小
- **-x**：最大文件锁数量
- **-P**：最大伪终端数量
- **-R**：实时进程阻塞前可以运行的最大时间
- **-T**：最大线程数量

**注意：**并非所有平台都支持以上所有选项。

如果指定了 **LIMIT**，则它表示指定资源的新值；特殊的 **LIMIT** 值包括：

- `soft`：当前软限制
- `hard`：当前硬限制
- `unlimited`：无限制

如果未指定 `LIMIT`，则输出指定资源的当前值；如果未给出选项，默认使用 `-f`。

**值单位：**

- 默认单位为 1024 字节增量。
- `-t` 的单位为秒。
- `-p` 的单位为 512 字节增量。
- `-u` 则是未缩放的进程数量。

**退出状态：**
返回成功，除非提供了无效选项或发生错误。

ulimit: ulimit [-SHabcdefiklmnpqrstuvxPRT] [limit]
Modify shell resource limits.

Provides control over the resources available to the shell and processes
it creates, on systems that allow such control.

Options:
-S        use the `soft' resource limit -H        use the `hard' resource limit
-a        all current limits are reported
-b        the socket buffer size
-c        the maximum size of core files created
-d        the maximum size of a process's data segment
-e        the maximum scheduling priority (`nice')
-f        the maximum size of files written by the shell and its children
-i        the maximum number of pending signals
-k        the maximum number of kqueues allocated for this process
-l        the maximum size a process may lock into memory
-m        the maximum resident set size
-n        the maximum number of open file descriptors
-p        the pipe buffer size
-q        the maximum number of bytes in POSIX message queues
-r        the maximum real-time scheduling priority
-s        the maximum stack size
-t        the maximum amount of cpu time in seconds
-u        the maximum number of user processes
-v        the size of virtual memory
-x        the maximum number of file locks
-P        the maximum number of pseudoterminals
-R        the maximum time a real-time process can run before blocking
-T        the maximum number of threads

Not all options are available on all platforms.

If LIMIT is given, it is the new value of the specified resource; the
special LIMIT values `soft', `hard', and `unlimited' stand for the
current soft limit, the current hard limit, and no limit, respectively.
Otherwise, the current value of the specified resource is printed.  If
no option is given, then -f is assumed.

Values are in 1024-byte increments, except for -t, which is in seconds,
-p, which is in increments of 512 bytes, and -u, which is an unscaled
number of processes.

Exit Status:
Returns success unless an invalid option is supplied or an error occurs.
