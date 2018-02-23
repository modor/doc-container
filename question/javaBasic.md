####  1.StringBuffer与StringBuilder有什么区别？
- 执行速度```StringBuilder``` > ```StringBuffer```  
- ```StringBuilder```是非线程安全的，```StringBuffer```是线程安全的。

#### 2.toString默认返回值是什么？
```
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

#### 3.hashCode()如何得到的？ 
默认情况下，```Object```中的```hashCode()```也是返回对象的32位jvm内存地址，但是```==```比较两个对象的时候并没有通过```hashCode()```方法获取，当然，也没法通过该方法获取，```==```是运算符，并不是```Object```对象的方法。

#### 4.equals()和==的区别？ 
在引用数据类型当中两者默认情况下本质是一样的，```Object```类中```equals()```方法就是调用了```==```，而```==```是比较两个对象的32位jvm内存地址。但```equals()```没法用于基本数据类型的比较，而```==```没法被重写，```String```类的比较之所以得到不同的结果是因为String数据类型默认重写了```equals()```方法。

#### 5.重写equals()方法时候为什么必须重写hashCode()方法？
- 和```hashCode()```方法的常规协定保持一致。
- 为了该对象能在哈希表中存储和检索，如果不重写hashCode()，那么存入的每个对象将会是不同的，该对象将再也没法被检索和删除，将会导致内存泄露。

### 6.List和Set区别？
- List有：ArrayList、LinkedList和Vector。Set分为HashSet和TreeSet；List可以重复，Set不可重复；HashSet底层实际上是HashMap的键值，TreeSet是TreeMap的键值，value存的都是new Objec()对象。
- add(),contains(),remove()时候List只调用的是equals()方法判断是否重复，Set则先调用hashCode()方法,再调用equals()方法。
- ArrayList在元素填满容器时会自动扩充容器大小的50%，而Vector则是100%，因此ArrayList更节省空间。

### 7.比较器有哪些使用方式？
- 继承Comparable接口，并实现compareTo()方法。
- 定义一个单独的对象比较器，继承自Comparator接口，实现compare()方法。

### 8.各个Map有什么区别？
- HashMap几乎可以等价于Hashtable，除了HashMap是非线程同步的，并可以接受null(HashMap可以接受为null的键值(key)和值(value)，而Hashtable则相反。
- 由于Hashtable是线程安全的也是synchronized，所以在单线程环境下它比HashMap要慢。
- ConcurrentHashMap融合了hashtable和hashmap二者的优势,但不能接受null。

### 9.异常和错误区别是什么？
- Throwable类是 Java语言中所有错误或异常的超类。
- Error用于标记严重错误，一般的应用程序不应该去try/catch这种错误，而是交给jvm处理。
- RuntimeException是可能在执行方法期间抛出但未被捕获的异常，RuntimeException的任何子类都无需在 throws子句中进行声明，也可以不用处理而交给jvm处理。除此之外其他Exception都需要进行异常捕获处理。

### 10.注解的使用和作用？
- JDK提供了四个元注解（1.8新增了类型注解和重复注解），通过四个元注解（@Documented、@Retention、@Target、@Inherited）和@interface关键字来定义自定义注解。
- JDK提供的常用注解有三个：@Override、@Deprecated、@SuppressWarnnings这三个注解由IDE和编译器来解析使用，这三个注解都是语法糖。
- 自定义注解的使用主要是运行时注解，一般是由框架通过反射来获取注解的值，进行校验或者注入到类中。
- 自定义注解支持的数据类型包括：所有基本数据类型、String类型、Class类型、enum类型、Annotation类型以及所有以上类型的数组。

### 11.ReenterLock的特点有哪几个？
- 可重入（重复使用，需要相应次数解锁）
- 可中断（lockInterruptibly）
- 可限时（tryLock）
- 公平锁（默认为非公平锁，若要使用公平锁，创建锁对象时候指定为true）

### 12.final关键字特点有哪些？
- final类不能被继承，没有子类，final类中的方法默认是final的。
- final方法不能被子类的方法覆盖，但可以被继承。
- final成员变量表示常量，只能被赋值一次，赋值后值不再改变。
- final不能用于修饰构造方法。
