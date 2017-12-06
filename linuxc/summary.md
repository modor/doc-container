####  1.gcc的使用
* -Wall输出所有警告信息
* -E gcc -E *.c -o *.i生成预处理文件
* -S gcc -S *.i -o *.s生成汇编文件
* -c gcc -c *.s -o *.o生成二进制文件
* -g gcc -g *.c -o name生成调试执行文件
* -O1 gcc -O1 *.c -o name选择优化级别，级别为1-3。

####  2.打包静态库
* gcc *.c -c -I../include
* ar rcs libMyLib.a *.o
* gcc main.c -Iinclude -L lib -l MyLib -o main(库名掐头去尾)

### 3.打包动态库
* gcc -fPIC -c *.c -I../include
* gcc -shared -o libMyLib.so *.o -Iinclude
* gcc main.c -Iinclude -L./lib -lMyLib -o main

### 4.内存分布
* ELF： .bss(未初始化全局变量) .data(已初始化全局变量) .text
* #define NULL (void*) 0 对应0-4k地址

### 5.线程查看
* ps -Lf pid