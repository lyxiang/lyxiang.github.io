---
layout: post
title: ArrayList、LinkedList、Vector的区别
categories: Java 集合
keywords: Java 集合
---

List 是一个接口，它继承于 Collection 接口。常用的实现类有：ArrayList，LinkedList，Vector。它表示有序且元素可重复的队列。而 Set 代表无序且元素不可重复的队列。List关注的是索引，拥有一系列和索引相关的方法，查询速度快。因为往 List 集合中间位置插入或删除数据时，会伴随着后面数据的移动，所以插入和删除数据速度较慢。通过之前的文章 [Java中的集合关系](https://lyxiang.github.io/2019/07/30/collection-ref/)，回顾下集合之间的关系。

---

## ArrayList
* ArrayList 的底层实现是基于动态数组的数据结构。我们知道，数组的长度在初始化之后，是不会发生变化的。这里的"可变数组"，实际上是 new 一个新的数组，将原来的数组内容 copy 到新的数组中。
* 每个 ArrayList 实例都有一个容量（Capacity），即用于存储元素的数组的大小。这个容量可随着不断添加新元素而自动增加，但是增长算法并没有定义。当需要插入大量元素时，在插入前可以调用ensureCapacity方法来增加ArrayList的容量以提高插入效率。
* ArrayList 允许插入所有元素，包括 NULL。
* ArrayList 是线程异步的，是线程不安全的。
* 优点：对于随机访问 get 和 set，ArrayList 要优于 LinkedList，因为 LinkedList 要移动指针。
* 缺点：在删除和添加元素时，需要考虑扩容和迁移数据，效率较低。

## LinkedList
* LinkedList 的底层实现是基于双向链表的数据结构。
* LinkedList 在数据插入和删除，只需要修改前后指针即可，性能较优。但是在查找和遍历，效率不如 ArrayList。
* LinkedList 是线程异步的，是线程不安全的。

## Vector
* Vector 的底层实现也是基于动态数组的数据结构。
* Vector 是线程同步的，也是线程安全的。
* 如果集合中的元素的数目大于目前集合数组的长度时，Vector 扩容长度为目前数组长度的100%，而 Arraylist扩容长度为目前数组长度的50%。如果在集合中使用数据量比较大的数据，用vector有一定的优势。

## SynchronizedList
* SynchronizedList 是工具类包collections提供的一个线程安全的List包装类。
* 利用 synchronized 关键字对List操作加锁，锁对象是自己本身。实现效率很低。

## 总结
* 如果查找一个指定位置的数据，Vector 和 Arraylist 使用的时间是相同的，如果频繁的访问数据，这个时候使用Vector 和 Arraylist 都可以。
* 如果需要频繁插入和删除元素，这个时候就应该考虑到使用 LinkedList, 因为它移动一个指定位置的数据时其它元素不移动。
* 如果使用场景并不要求线程安全，优先使用 ArrayList 和 LinkedList。因为 Vector 是线程同步的，相比会花费更多的性能。

