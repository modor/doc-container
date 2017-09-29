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
- 为了该对象能在哈希表中存储和检索。

