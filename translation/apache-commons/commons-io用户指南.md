## 用户指南
Commons-IO可以划分为utility classes（实用工具类）, endian classes（端排序类）, line iterator（行迭代器）, file filters（文件过滤器）, file comparators（文件比较器）和stream implementations（流实现类）。更多的细节描述请看[javadoc](https://commons.apache.org/proper/commons-io/javadocs/api-release/index.html)。  
## Utility classes（实用工具类）
### IOUtils
IOUtils类包含了处理流读取、写入和拷贝的通用方法。这些方法处理的流包括InputStream, OutputStream, Reader和Writer。让我们思考一下如何从一个URL中读取数据流并输出其读取内容。一般实现方法如下：
```
InputStream in = new URL( "http://commons.apache.org" ).openStream();
try{
   InputStreamReader inR = new InputStreamReader( in );
   BufferedReader buf = new BufferedReader( inR );
   String line;
   while(( line = buf.readLine() ) != null ){
     System.out.println( line );
   }
}finally{
   in.close();
}
```
使用IOUtils可以简写成如下：
```
InputStream in = new URL( "http://commons.apache.org" ).openStream();
try{
   System.out.println( IOUtils.toString( in ) );
}finally{
   IOUtils.closeQuietly(in);
}
```
在固定应用中，像这种IO操作是通用的，使用IOUtils可以节省大量时间。而且其代码是经过测试、经得起推敲的。  
对于这种工具集来说，灵活性和速度都是同样重要的。我们应该明白工具的使用都是有局限性的。如IOUtils，如果用它试图读取一个1GB的文件就相当于创建一个占内存1GB的对象（大文件可能导致内存溢出）。
### FileUtils
FileUtils类包含了操作文件对象的方法，包括对文件的读、写、拷贝以及文件比较等操作。
下面例子展示了如何去读取一个文件的一整行：
```
File file = new File("/commons/io/project.properties");
List lines = FileUtils.readLines(file, "UTF-8");
```
### FilenameUtils
FilenameUtils主要用来操作文件名字而不是文件对象本身。这个类的主要作用是协调Unix和Windows系统，让文件名字和路径在这两个环境之间相互转换（如开发环境Windows转到生产环境Linux）。  
下面一个例子是去掉两点分隔符，标准化一个文件名的过程（两点分割符代表上一级目录）。
```
String filename = "C:/commons/io/../lang/project.xml";
String normalized = FilenameUtils.normalize(filename);
// result is "C:/commons/lang/project.xml"
```
### FileSystemUtils
FileSystemUtils类包含了一些JDK不支持的对文件系统的操作。目前FileSystemUtils只有一个获取驱动器（磁盘）剩余空间的方法。通常情况下，这些信息只能通过命令行获取，而无法通过本地代码获取。  
如下面例子，查询一个驱动器剩余的空间：
```
long freeSpace = FileSystemUtils.freeSpace("C:/");
```  
## Endian classes（端排序类）
不同的计算机架构有不同的字节默认排序方式。小端架构是指低字节被存储在内存的低地址段，高字节则存储在高地址段。大端排序则情况相反。  
在端排序的包中有两个类：
* EndianUtils 包含了转换java基本数据和流大小端的静态方法。
* SwappedDataInputStream是接口DataInput的实现。我们可以使用它读取非本地端排序的数据。更多信息, 请见 http://www.cs.umass.edu/~verts/cs32/endian.html

## Line iterator（行迭代器）
org.apache.commons.io.LineIterator对于基于行访问文件提供了另外一种灵活的方式。一个文件可以直接创建，也可以通过FileUtils或者IOUtils的工厂方法创建。惯用方式如下：
```
LineIterator it = FileUtils.lineIterator(file, "UTF-8");
try{
    while (it.hasNext()) {
     String line = it.nextLine();
     /// do something with line
    }
} finally {
    LineIterator.closeQuietly(iterator);
}
```
## File filters(文件过滤器)
org.apache.commons.io.filefilter包定义了一个将java.io.FileFilter和java.io.FilenameFilter组合起来的接口。除此之外，该包还提供了一些列已经可以直接使用
的IOFileFilter的实现。这些接口和实现可以和其他过滤器组合使用。例如，可以和一些列出文件或者文件对话框组合使用。  
更详细filefilter包内容请看javadoc。

## File comparators（文件比较器）
org.apache.commons.io.comparator包为java.io.File提供了一系列java.util.Comparator接口的实现。例如，这些实现的比较器可以用来排序列表和数组中的文件。  
更详细comparator包内容请看javadoc。

## Streams（流）
org.apache.commons.io.input和org.apache.commons.io.output包包含了一些非常有用的流的实现。包括：
* 空输出流 - 可以接收所有发送给它的数据（类似于linux中的/dev/null文件）。
* 双输出流 - 可以发送数据到两个流（输入一组数据，产生两个流，类似T字母）。
* 字节数组输出流 - 这是一个比jdk自带版本更快的版本。
* 统计流 - 计算通过流的的字节数。
* 代理流 - 将流委派给代理中正确的方法处理。
* 写锁 - 提供一个同步写文件的锁。

更详细输入输出包信息请参加javadoc。

**原文地址：** https://commons.apache.org/proper/commons-io/description.html