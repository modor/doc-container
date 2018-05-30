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

### 4.动态库的使用
* 程序通过/lib64/ld-linux-x86-64.so.2来管理动态库依赖，lddconfig -v来查看当前的动态库有哪些。
* 动态库管理库首先会去LD_LIBRARY_PATH中寻找程序依赖动态库是否存在，若不存在则去动态库配置文件/etc/ld.so.conf中寻找，若仍然找不到则会去系统PATH中寻找。

### 5.编译时头文件路径检索顺序	
* -I或-L指定的路径。
* gcc的环境变量定义路径C_INCLUDE_PATH, CPLUS_INCLUDE_PATH, OBJC_INCLUDE_PATH。
* 内定目录 /usr/include和/usr/local/include。

### 6.内存分布
* ELF： .bss(未初始化全局变量) .data(已初始化全局变量) .text
* #define NULL (void*) 0 对应0-4k地址

### 7.线程查看
* ps -Lf pid