Java常用技术简要
===
&emsp;&emsp;本文旨在收集平时开发中常用的基础技术，方便查阅。  

Java RMI框架（远程方法调用）
-----
&emsp;&emsp;Java RMI不是什么新技术（在Java1.1的时代都有了），但却是是非常重要的底层技术。EJB技术以及RPC框架Dubbo、Thrift都是基于该技术。对外提供Java　Rmi分三步：  
1）定义一个继承了Remote远程接口。  
2）实现该远程接口，实现类必须继承UnicastRemoteObject类。  
3）创建RMI注册表，启动RMI服务，并将远程对象注册到RMI注册表中。  

***
双亲委派机制
-----
* 加载器类型:   
1）Bootstrap ClassLoader 最顶层的加载类，主要加载%JRE_HOME%\lib下的核心类库。  
2）Extention ClassLoader 扩展的类加载器，加载目录%JRE_HOME%\lib\ext目录下的jar包和class文件。  
3）Appclass ClassLoader  也称为SystemAppClass 加载当前应用的classpath的所有类。  
4）自定义ClassLoader。  
* 双亲委派概念  
&emsp;&emsp;这是四个加载器按照先后默认使用顺序列出的，本层的上一层加载器叫做该层的父加载器。当一个类加载器收到了类加载的请求时，它会先查找该类是否已经加载，如果没有加载它也并不会先加载该类，而是把该类交给父类进行查找，父类也是进行如此动作，如果已经加载则直接返回，若没有则会一直查找到最顶层Bootstrap ClassLoader，若都没有加载该类，则返回到相应的可以加载该类的层进行该类的加载，这种机制叫做双亲委派机制。
* 破坏双亲委派  
&emsp;&emsp;破坏双亲委派是指在自定义加载器中破坏，默认自义定加载器只需继承ClassLoader类，然后重写findClass方法即可。而打破双亲委派机制则不仅要继承ClassLoader类，loadClass和findClass方法都要重写，以破坏loadClass中在找不到该类时把加载查询交给父加载器。
***
类加载时机
-----
* 遇到new、getstatic、putstatic或invokestatic指令时：即new关键字实例化对象的时候和读取或者设置一个静态字段的时候（final修饰除外）。
* 反射调用时：即调用Class.forname("className")、类名.class.newInstance()时。
* 虚拟机启动时会加载含有main()方法的类。
* 使用jdk1.7动态语言支持时。
***
内存溢出
-----
* 堆溢出  
Java不停的创建对象或者内存泄露会导致堆溢出，使用内存映像分析工具（如Eclipse Memory Analyzer）堆Dump出来的堆转储快照进行分析，查看是内存泄露还是内存溢出。
* 栈溢出  
栈溢出一般是递归调用超过了虚拟机所允许的最大深度，需要检查递归调用，减少其调用深度。
* 运行时常量池溢出  
运行时常量池是方法区的一部分，所以在运行时常量池溢出时候会报永久代空间不足。
***

阻塞队列
-----
&emsp;&emsp;阻塞队列共有五个类：ArrayBlockingQueue、DelayQueue、LinkedBlockingQueue、PriorityBlockingQueue、SynchronousQueue都实现了BlockingQueue接口。
* ArrayBlockingQueue 是一个有界的阻塞队列，其内部实现是将对象放到一个数组里，具有数组特性，初始化时候就需要指定大小，一旦初始化，大小就无法修改。
* DelayQueue 对元素进行持有直到一个特定的延迟到期。注入其中的元素必须实现 java.util.concurrent.Delayed 接口。
* LinkedBlockingQueue内部以一个链式结构(链接节点)对其元素进行存储。理性情况是没有数量限制的，如果需要的话，这一链式结构可以选择一个上限。如果没有定义上限，将使用 Integer.MAX_VALUE作为上限。
* PriorityBlockingQueue是一个无界的并发队列。它使用了和类 java.util.PriorityQueue 一样的排序规则。你无法向这个队列中插入 null 值。所有插入到 PriorityBlockingQueue 的元素必须实现 java.lang.Comparable 接口。因此该队列中元素的排序就取决于你自己的 Comparable实现。
* SynchronousQueue是一个特殊的队列，它的内部同时只能够容纳单个元素。如果该队列已有一元素的话，试图向队列中插入一个新元素的线程将会阻塞，直到另一个线程将该元素从队列中抽走。同样，如果该队列为空，试图向队列中抽取一个元素的线程将会阻塞，直到另一个线程向队列中插入了一条新的元素。
***
