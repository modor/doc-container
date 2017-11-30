####  1.gcc的使用
* -Wall输出所有警告信息
* -E gcc -E *.c -o *.i生成预处理文件
* -S gcc -S *.i -o *.s生成汇编文件
* -c gcc -c *.s -o *.o生成二进制文件
* -g gcc -g *.c -o name生成调试执行文件
* -O1 gcc -O1 *.c -o name选择优化级别，级别为1-3。

