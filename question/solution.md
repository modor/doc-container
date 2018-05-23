## java基础
###  1.List和 Set的区别.
ArrayList的底层实现是数组、LinkedList是链表；HashSet的底层实现是散列表，TreeSet的底层实现的红黑树；

### 2.HashSet是如何保证不重复的。
存入一个元素时候会先比较自身的hashCode，如果hashCode相同，则调用equals方法进行比较，也相同的话就会丢弃不存入，不相同就会存入。TreeSet则会调用compare方法进行比较排序。

### 3.HashMap什么不是线程安全的。

### 4.HashMap的扩容过程
HashMap初始容量大小为16，jdk1.8在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。原本Map.Entry接口的实现类Entry改名为了Node。转化为红黑树时改用另一种实现TreeNode。 

### 5.HashMap1.7与1.8的区别。

### 6.final、finally、finalize区别。
1)final类不能被继承；final方法不能被子类的方法覆盖；final成员变量表示常量，只能被赋值一次；赋值后值不再改变；final不能用于修饰构造方法。
2)finally和try catch配合使用，用户异常后动作处理。
3)finalize会触发垃圾收集器执行垃圾回收动作。

### 7.强引用 、软引用、 弱引用、虚引用。

### 8.Java反射

### 9.Arrays.sort实现原理和 Collection实现原理。

### 10.LinkedHashMap的应用。

### 11.cloneable接口实现原理。

### 12.异常分类以及处理机制。

### 13.wait和sleep的区别。

### 14.数组在内存中如何分配。

## Java并发
### 1.synchronized的实现原理以及锁优化。
同步代码块是使用monitorenter和monitorexit指令实现的,synchronized用的锁是存在Java对象头里的；在获取锁的时候会先比较对象头里的Mark Word，如果一致则获取锁，这个过程是偏向锁，如果不一致则进入自旋，竞争获取锁，这就进入了轻量级锁，如果自旋仍然获取锁失败，则进入阻塞，等待jvm分配锁，这就进入了重量级锁。

### 2.volatile的实现原理。
volatile是缓存一致性协议的的实现，可以保证可见性、顺序性、一致性，但无法保证原子性，volatile使用场景并不多，只有一些初始化的场景中因为使用synchronized锁较重量级时会用到，synchronized在保证缓存一致性（可见性）的同时，也保证了原子性。

### 3.Java的信号灯。


### 4.synchronized在静态方法和普通方法的区别。
synchronized用在普通方法上是在对象上加锁，位于堆里面；用在静态方法的时候，锁位于类里面，即代码区（永久代）内。

### 5.怎么实现所有线程在等待某个事件的发生才会去执行。
### 6.CAS有什么缺陷，如何解决。
### 7.synchronized和lock有什么区别。
### 8.Hashtable是怎么加锁的。
### 9.HashMap的并发问题。
### 10.ConcurrenHashMap在1.8中为什么要用红黑树。
### 11.AQS。
### 12.如何检测死锁？怎么预防死锁？
### 13.Java内存模型？ 
### 14.如何保证多线程下i++结果正确？
### 15.线程池的种类，区别和使用场景？
### 16.分析线程池的实现原理和线程的调度过程？
### 17.线程池如何调优，最大数目如何确认？
### 18.ThreadLocal原理，用的时候需要注意什么？
### 19.CountDownLatch和 CyclicBarrier的用法，以及相互之间的差别？
### 20.LockSupport工具。
### 21.Condition接口及其实现原理。
### 22.Fork/Join框架的理解。
### 23.分段锁的原理,锁力度减小的思考。
### 24.八种阻塞队列以及各个阻塞队列的特性。

## 关于Spring
1.BeanFactory和FactoryBean。
2.Spring IOC的理解，其初始化过程。
3.BeanFactory和 ApplicationContext。
4.Spring Bean的生命周期，如何被管理的。
5.Spring Bean的加载过程是怎样的。
6.如果要你实现Spring AOP，请问怎么实现。
7.如果要你实现Spring IOC，你会注意哪些问题。
8.Spring是如何管理事务的，事务管理机制。
Spring并不直接管理事务，而是提供了多种事务管理器，Spring事务管理器的接口是org.springframework.transaction.PlatformTransactionManager，通过这个接口，Spring为各个平台如JDBC、Hibernate等都提供了对应的事务管理器，但是具体的实现就是各个平台自己的事情了

9.Spring的不同事务传播行为有哪些，干什么用的。
10.Spring中用到了那些设计模式。
11.SpringMVC的工作原理。
12.Spring循环注入的原理。
13.SpringAOP的理解，各个术语，他们是怎么相互工作的。
14.Spring如何保证 Controller并发的安全。

## 关于Netty
1.BIO、NIO和AIO。
2.Netty 的各大组件。
3.Netty的线程模型。
4.TCP粘包/拆包的原因及解决方法。
5.了解哪几种序列化协议？包括使用场景和如何去选择。
6.Netty的零拷贝实现。
7.Netty的高性能表现在哪些方面。
8.http协议的content-length。
1）服务器已经知道资源大小，通过content-length这个header告诉你。 
2）服务器没法提前知道资源的大小，或者不愿意花费资源提前计算资源大小，就会把http回复报文中加一个header叫Transfer-Encoding:chunked，就是分块传输的意思。每一块都使用固定的格式，前边是块的大小，后面是数据，然后最后一块大小是0。这样客户端解析的时候就需要注意去掉一些无用的字段。 
3）服务器不知道资源的大小，同时也不支持chunked的传输模式，那么就既没有content-length头，也没有transfer-encoding头，这种情况下必须使用短连接，以连接结束来标示数据传输结束，传输结束就能知道大小了。这时候服务器返回的header里Connection一定是close。

## 分布式相关
1.Dubbo的底层实现原理和机制。
2.描述一个服务从发布到被消费的详细过程。
3.分布式系统怎么做服务治理。
4.接口的幂等性的概念。
5.消息中间件如何解决消息丢失问题。
6.Dubbo的服务请求失败怎么处理。
7.重连机制会不会造成错误。
8.对分布式事务的理解。
9.如何实现负载均衡，有哪些算法可以实现？
10.Zookeeper的用途，选举的原理是什么？
11.数据的垂直拆分水平拆分。
12.zookeeper原理和适用场景。
13.zookeeper watch机制。
14.redis/zk节点宕机如何处理。
15.分布式集群下如何做到唯一序列号。
16.如何做一个分布式锁。
17.用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗。
18.MQ系统的数据如何保证不丢失。
19.列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题。
20.zookeeper的选举策略。
21.全局ID。
22.raft算法原理及脑裂解决思路。

## 数据库
1.mysql分页有什么优化。
1）页码和主键关联，然后使用between and来替代limit查询。
2）id建立索引，然后先查询出id所在行，然后利用子查询的形式（id>=）来查询，如：SELECT * FROM product WHERE ID > =(select id from product limit 866613, 1) limit 20。

2.悲观锁、乐观锁。
3.组合索引，最左原则。
4.mysql的表锁、行锁。
5.mysql性能优化。
6.mysql的索引分类：B+，hash；什么情况用什么索引。
7.事务的特性和隔离级别。
1）Read uncommitted  
2）Read committed  
3）Repeatable read  
4）Serializable  
大多数数据库默认的事务隔离级别是Read committed，比如Sql Server, Oracle。Mysql的默认隔离级别是Repeatable read。

## 关于缓存
1.Redis用过哪些数据数据，以及Redis底层怎么实现。
2.Redis缓存穿透，缓存雪崩。
3.如何使用Redis来实现分布式锁。
4.Redis的并发竞争问题如何解决。
5.Redis持久化的几种方式，优缺点是什么，怎么实现的。
6.Redis的缓存失效策略。
7.Redis集群，高可用，原理。
8.Redis缓存分片。
9.Redis的数据淘汰策略。
10.如何解决redis脑裂问题

## 关于JVM
1.详细jvm内存模型。
2.讲讲什么情况下回出现内存溢出，内存泄漏。
3.说说Java线程栈。
4.JVM年轻代到年老代的晋升过程的判断条件是什么呢。
5.JVM出现 fullGC很频繁，怎么去线上排查问题。
6.类加载为什么要使用双亲委派模式，有没有什么场景是打破了这个模式。
7.类的实例化顺序。
8.JVM垃圾回收机制，何时触发MinorGC等操作。
9.JVM 中一次完整的 GC 流程（从 ygc 到 fgc）是怎样的。
10.各种回收器，各自优缺点，重点CMS、G1。
11.各种回收算法。
12.OOM错误，stackoverflow错误，permgen space错误。

## 其他情况
1.高可用方案之脑裂问题。
1）添加冗余的心跳线，例如双线条线，尽量减少“裂脑”发生机会。
2）启用磁盘锁，正在服务一方锁住共享磁盘，“裂脑”发生时，让对方完全“抢不走”共享磁盘资源。
3）设置仲裁机制。例如设置参考IP（如网关IP），当心跳线完全断开时，2个节点都各自ping一下 参考IP，不通则表明断点就出在本端。