---
title: HashTable和HashMap的区别
layout: post

description: "HashSet 实现了 Set 接口，它不允许集合中有重复的值,HashMap 实现了 Map 接口，Map 接口对键值对进行映射。Map 中不允许重复的键。"
redirect_from: ["/2017/07/27/hashtableandhashmap.html"]

---
* #### 什么是HashMap ##  
HashSet 实现了 Set 接口，它不允许集合中有重复的值，当我们提到 HashSet 时，第一件事情就是在将对象存储在 HashSet 之前，要先确保对象重写 equals()和 hashCode()方法，这样才能比较对象的值是否相等，以确保set中没有储存相等的对象。如果我们没有重写这两个方法，将会使用这个方法的默认实现。
public boolean add(Object o)方法用来在 Set 中添加元素，当元素值重复时则会立即返回 false，如果成功添加的话会返回 true。  

HashMap是基于哈希表的Map接口非同步实现, 此实现提供可选的映射操作,允许null值和null建.
不保证映射的顺序,且不保证顺序不会改变.
HashMap不是同步的,如果多个线程同时访问一个HashMap,如果其中至少有一个现象对该HashMap对象做出了结构上的改变(添加或者删除), 则必须要保持外部(访问该HashMap的方法)同步,防止非同步访问

HashMap的实现原理(数据结构)
HashMap的数据实际是存放在一个Node的对象(静态内部类)数据组中, 这个node对象中存放了key和value还有hash值和next下一个node节点
Node实现了Map接口的一个内部接口Entry
![](/res/0727/node.png)
构造函数 (初始化大小,加载因子)    HashMap 默认大小为16加载因子是0.75  

![](/res/0727/init.png)  
遍历一个HashMap的方法  
![](/res/0727/iterator.png)    
![](/res/0727/entrySet.png)  
![](/res/0727/foreach.png)   
entrySet的方式效率比较高
for方法比较简洁且高效,我倾向于这种方法,只需要迭代key就使用第一种方法.




* #### 什么是HashTable  

HashMap 实现了 Map 接口，Map 接口对键值对进行映射。Map 中不允许重复的键。Map 接口有两个基本的实现，HashMap 和 TreeMap。TreeMap 保存了对象的排列次序，而 HashMap 则不能。HashMap 允许键和值为 null。HashMap 是非 synchronized 的，但 collection 框架提供方法能保证 HashMap synchronized，这样多个线程同时访问 HashMap 时，能保证只有一个线程更改 Map。
public Object put(Object Key,Object value)方法用来将元素添加到 map 中。

HashSet是基于HashMap实现的，底层是用HashMap来保存元素的.
查看其源码可见是在构造函数中直接new了一个HashMap对象并赋给了table,table是HashSet的一个成员属性

![](/res/0727/method.png)    
对HashSet的各种方法的操作底层实际操作的都是对HashMap的操作
![](/res/0727/mapfield.png)  
![](/res/0727/size.png)  
![](/res/0727/isempty.png)  
![](/res/0727/add.png)    
迭代HashSet其实就是迭代HashMap的Key值
![](/res/0727/HashTableIterator.png)




* ### 个人总结  
 1. 师从不一样, HashMap实现的是Map接口,HashSet实现了Set接口
 2. 存储数据的形式不一样, HashMap 是存放的键值对, HashSet存放的是对象
 3. 存放数据用的方法不一样, HashMap用put方法HashSet用add方法
 4. HashMap可以通过键值key用get方法获取到其中的一个数据,而HashSet只能通过遍历

 ==========================================================
 HashMap中key是不允许重复的（后面的会覆盖原有的键值）, HashSet中的值不能重复,因为其中的数据就是通过HashMap的key存储的
 所以当需要使用Set存储对象类型的数据时,为了确保没有重复的数据需要重写该对象的hashCode和 equals方法,
 同理,如果需要用对象类型的数据作为Map的key时,需要重写该对象类的HashCode和equals方法,确保唯一性,, sososo一般用String类型作为Key因为String类型是final的


![](/res/0727/samekey.png)


参考
[http://www.runoob.com/java/java-collections.html](http://www.runoob.com/java/java-collections.html)  
[http://wiki.jikexueyuan.com/project/java-collection/hashset-and-hashmap.html](http://wiki.jikexueyuan.com/project/java-collection/hashset-and-hashmap.html)


### 联系我
 * email : [ilxj20@163.com](mailto:ilxj20@163.com?subject=sen to Moss&body=邮件内容)
 <!-- subject后面不能跟中文,否则后果很杯具-->
