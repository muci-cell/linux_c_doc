`gcc`（GNU Compiler Collection）是一个常用的 C 和 C++ 编译器，使用它进行编译时可以使用多种指令和选项。以下是一些常见的 `gcc` 编译指令及其功能：

### 基本编译指令

1. **编译源文件**：

   ```bash
   gcc source.c -o output
   ```

   这将编译 `source.c` 文件并生成可执行文件 `output`。
2. **编译并输出调试信息**：

   ```bash
   gcc -g source.c -o output
   ```

   添加 `-g` 选项会在可执行文件中包含调试信息，便于使用调试器（如 `gdb`）调试。
3. **优化选项**：

   ```bash
   gcc -O2 source.c -o output
   ```

   使用 `-O` 选项可以开启优化，`-O2` 是常用的优化级别，具体可选级别有：

   - `-O0`：不优化（默认）。
   - `-O1`：基本优化。
   - `-O2`：中等优化，常用。
   - `-O3`：高级优化，可能会增加编译时间和可执行文件大小。
4. **指定标准**：

   ```bash
   gcc -std=c99 source.c -o output
   ```

   使用 `-std` 选项可以指定 C 标准（如 `c89`, `c99`, `c11`, `c18` 等）。
5. **包含目录**：

   ```bash
   gcc -I/path/to/include source.c -o output
   ```

   使用 `-I` 选项指定额外的头文件搜索路径。
6. **链接库**：

   ```bash
   gcc source.c -o output -lm
   ```

   使用 `-l` 选项链接库，如 `-lm` 链接数学库。
7. **预处理**：

   ```bash
   gcc -E source.c -o output.i
   ```

   使用 `-E` 选项仅执行预处理，生成预处理文件 `output.i`。
8. **生成汇编代码**：

   ```bash
   gcc -S source.c -o output.s
   ```

   使用 `-S` 选项生成汇编代码文件 `output.s`。
9. **编译多个文件**：

   ```bash
   gcc file1.c file2.c -o output
   ```

   可以同时编译多个源文件。

### 其他常用选项

- **`-Wall`**：启用所有警告信息。
- **`-Werror`**：将警告视为错误，编译失败。
- **`-o filename`**：指定输出文件名。
- **`-l<library>`**：链接指定的库，例如 `-lpthread` 链接 POSIX 线程库。

使用 `man gcc` 可以查看更详细的文档，获取更多选项和功能的说明。
