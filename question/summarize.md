####  1.运维转开发优势心得？
- 对网络、架构、集群、分布式等概念理解更加深刻。
- 对linux系统很熟悉，为后续了解系统，学习系统开发打下基础。
- 对代码开发中某些代码对系统整体影响理解更加深刻。

####  2.Web应用框架需要解决的问题？
1）数据绑定（简单类型、包装类、数组、复杂对象、List、Set、Map、Json、Xml、数据转换器）  
2）数据校验（jsr303、Hibernate validator）  
3）url映射（普通url、restful）  
4）拦截器验证  
5）统一异常处理  
6）域对象传递  
7）统一编码处理  
8）国际化处理方式  

####  3.ORM框架需要解决的问题？
1）缓存问题  
2）查询数据映射对象问题  
3）事务处理问题  

####  4.并发工具包要解决的问题？
1）同步器：为特定的同步问题提供解决方案。  
2）执行器：用来管理线程的执行。  
3）并发集合：提供集合框架并发版本。  
4）Fork/Join框架：提供对并行编程的支持。  
5）atomic包：提供了不需要锁即可完成并发环境变量使用的原子操作。  
6）locks包：提供了传统锁的另一种替代方案。  

####  5.并发工具包内工具分类？
1）同步器
（信号量，new Semaphore(n),acquire(),release()）  
（计数栓，new CoundDownLatch(n),await(),countDown()）  
（循环屏障，new CyclicBarrier(n,thread),await(),等待数量达到n,则开始执行thread）  
（交换器，两个线程传入new Exchanger(),通过exchange(obj),交换对象）  
（Phaser，替代CoundDownLatch和CyclicBarrier）  
2）执行器：  
3）并发集合：  
（ConcurrentHashMap:比HashTable效率高）  
（ConcurrentLinkedQueue:非阻塞队列）  
（BlockingQueue:ArrayDeque(数组双端队列)、PriorityQueue(优先级队列)、PriorityQueue(优先级队列)、ConcurrentLinkedQueue(基于链表的并发队列)、DelayQueue(延期阻塞队列)、ArrayBlockingQueue(基于数组的并发阻塞队列)、LinkedBlockingQueue(基于链表的FIFO阻塞队列)、LinkedBlockingDeque(基于链表的FIFO双端阻塞队列)、PriorityBlockingQueue(带优先级的无界阻塞队列)、SynchronousQueue(并发同步阻塞队列)）  
4）Fork/Join框架：  
5）atomic包：  
（AtomicBoolean:原子更新布尔类型，AtomicInteger:原子更新整型，AtomicLong:原子更新整型）  
（AtomicIntegerArray:原子更新整型数组里的元素，AtomicLongArray:原子更新长整型数组里的元素，AtomicReferenceArray:原子更新引用类型数组里的元素，）  
（AtomicReference:原子更新引用类型，AtomicReferenceFieldUpdater:原子更新引用类型里的字段，AtomicMarkableReference:原子更新带有标记为的引用类型）  
（AtomicIntegerFieldUpdater:原子更新整型的字段的更新器，AtomicLongFieldUpdater:原子更新长整型的字段的更新器，AtomicStampedReference:原子更新带有版本号的引用类型）  
6）locks包：  