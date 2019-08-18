---
layout: post
title: HashMap、HashTable、ConcurrentHashMap的区别
categories: Java 集合
keywords: Java 集合
---

在 Java 中，Map 是一个顶级接口。常用的实现类有 HashMap，HashTable，ConcurrentHashMap 等。本文主要罗列常用的HashMap、HashSet、ConcurrentHashMap和HashTable之间的区别。在面试中，这几种Map的实现类之间的区别，也是被经常问到的一个很重要的知识点。

---

## HashMap和HaspTable的区别
* HashMap 和 HashTable 底层实现的数据结构都是：数组加链表。
* HashTable 是线程安全的，HashMap是线程不安全的。HashTable实现线程安全的策略是，在方法前面加synchronized来做同步。
* HashTable 的 key 和 value 都不允许为 null。而HashMap允许 key 和 value 为null。
* HashTable 的 hash 数组默认值是11，扩充的方式是 oldsize^2+1。而 HashTable 的 hash 数组默认长度是16，而且一定是2的倍数，扩充方式是 oldsize*2。
* HashTable 使用 Enumeration 进行遍历，HashMap 使用 Iterator 进行遍历。
* HashTable 的 hash 值是 key 的 hash 值，而 HashMap 的 hash 值是对 key 的 hash 进行运算，得到一个新的数值。

## HashMap和HashSet的区别
* HashSet 的底层实现是采用 HashMap 实现的。
* HashSet#add 就是 HashMap#put 的调用， key 就是要插入的值， value就是常量对象。

## HashMap和ConcurrentHashMap的区别
* HashMap 和 ConcurrentHashMap 底层实现的数据结构都是：数组加链表。
* ConcurrentHashMap 是线程安全的，HashMap是线程不安全的。
* ConcurrentHashMap 的 key 和 value 都不允许为 null。而 HashMap 允许 key 和 value 为null。
* ConcurrentHashMap 的加锁粒度比 HashTable 更精细，是加载某一块数据的。HashTable 是直接加载方法上的。ConcurrentHashMap 的效率远高于 HashTable。
* 在并发操作中，常用 ConcurrentHashMap。

## 总结
* 如果是在并发操作下，建议使用 ConcurrentHashMap。
* 在 Map 的迭代过程中，不建议删除元素。