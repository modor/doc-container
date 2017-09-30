## 用户指南
Commons-Collections为我们日常编程提供了大量的工具类，该文档为新手着重展示了该工具类的一些主要特性。
* 标准collections（集合）的工具类
* Maps
  * Map迭代器
  * 有序Map
  * 双向Map
* Bags

## 关于同步
Commons-collections使用的同步方式和标准的Java集合同步方式类似。主要的几个接口实现类，包括maps和bags在没有额外加锁的情况下都是非线程安全的。我们可以通过给这些实现类加上适当的锁方法来实现多线程时候的同步。  
类一级的javadocs应当说明：多线程的时候，在没有额外加锁的情况下使用一个特定类是否是线程安全的。如果没有特别指出一个实现类是线程安全的，那么在使用它的时候默认应该是需要加锁的。若文档有遗漏，请将遗漏发送给commons开发组。

## 实用类
实用类可以应用于每一个主要的集合接口。像```SetUtils```应用于```Set```和```SortedSet```接口.这些类为各种集合类型提供了可用的工具方法。  
大多数方法可以在两个根集合（Collection和Map）的使用类-CollectionUtils和MapUtils中找到。其他继承了Collection和Map接口的也可以使用使用这些工具类。包括类中的插入、计数、迭代、函子以及类型转换操作也可以使用这些工具。这些实用类还提供了类似于JDK中```Collections```类的功能来访问集合的装饰类。

## Maps
### Map迭代器
JDK默认的Map接口的迭代器使用起来总是有些绕。API使用者总是被强迫通过EntrySet或者KeySet进行迭代查询。Commons-Collections现在提供了一个新的接口-```MapIterator```，它一通过简单的方式对maps进行迭代。
```
IterableMap map = new HashedMap();
MapIterator it = map.mapIterator();
while (it.hasNext()) {
  Object key = it.next();
  Object value = it.getValue();
  
  it.setValue(newValue);
}
```
### 有序Maps
这个接口为那些没有排序功能接口提供了排序方法：```OrderedMap```。同时，为Map接口提供了两个实现类：```LinkedMap```和```ListOrderedMap```（装饰器模式）。这个接口支持map的迭代，而且允许迭代器向前和向后遍历map。
```
OrderedMap map = new LinkedMap();
map.put("FIVE", "5");
map.put("SIX", "6");
map.put("SEVEN", "7");
map.firstKey();  // returns "FIVE"
map.nextKey("FIVE");  // returns "SIX"
map.nextKey("SIX");  // returns "SEVEN"
```
### 双向Maps
```BidiMap```支持双向maps。这种maps可以通过key查询到value，也可以通过value查询到key。
```
BidiMap bidi = new TreeBidiMap();
bidi.put("SIX", "6");
bidi.get("SIX");  // returns "6"
bidi.getKey("6");  // returns "SIX"
bidi.removeValue("6");  // removes the mapping
BidiMap inverse = bidi.inverseBidiMap();  // returns a map with keys and values swapped
```
此外，还提供了双向maps的排序接口，为每种双向map类型都提供了排序的实现类。

### Bags
```Bag```支持bags，这种集合类会为存在里面的元素保存一定数量的副本。
```
Bag bag = new HashBag();
bag.add("ONE", 6);  // add 6 copies of "ONE"
bag.remove("ONE", 2);  // removes 2 copies of "ONE"
bag.getCount("ONE");  // returns 4, the number of copies in the bag (6 - 2)
```
Commons-Collections为能排序和不能排序的Bags都提供了实现。  
**原文地址：** https://commons.apache.org/proper/commons-collections/userguide.html
