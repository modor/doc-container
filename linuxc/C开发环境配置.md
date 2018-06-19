####  1.安装配置man手册
yum install man  man-pages-zh-CN -y

####  2.安装开发调试环境
yum install vim gcc gdb -y

### 3.安装跳转插件和对齐工具
yum install ctags indent -y

### 4.常用操作
* 代码补全：ctrl+p、ctrl+n（整行补全：ctrl+x然后ctrl+l）
* 查看当前函数man手册：shift+k
* 执行shell查看man：!man 3 open
* 生成跳转索引：ctags -R *
* 函数跳转和返回：ctrl+]、ctrl+t

### 5.其他
* 目录管理插件：NERDTree
* 源代码概览插件：Taglist
* 语法补全插件：Supertab
* 插件管理插件：Pathogen