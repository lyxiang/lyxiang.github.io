---
layout: post
title: 集合的fail-fast和fail-safe
categories: Java 集合 
keywords: Java 集合 并发
---

在我们详细讨论这两种机制的区别之前，首先得先了解并发修改。

---

## 并发修改
当一个或多个线程正在遍历一个集合Collection，此时另一个线程修改了这个集合的内容（添加，删除或者修改）。

## fail-fast机制

* 定义：在系统设计中，快速失效系统一种可以立即报告任何可能表明故障的情况的系统。快速失效系统通常设计用于停止正常操作，而不是试图继续可能存在缺陷的过程。这种设计通常会在操作中的多个点检查系统的状态，因此可以及早检测到任何故障。快速失败模块的职责是检测错误，然后让系统的下一个最高级别处理错误。
* 概念：fail-fase是集合的一种错误机制，当多个线程对同一个集合内容进行操作时，就可能会出现fail-fast情况。

以 ArrayList 为例，分析fail-fast机制：

![ArrayList的遍历源码](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/ArrayList_001.png)

从上图源码中可知，迭代器在调用next()的方法的时候，会调用checkForComodification()方法，检查expectedModCount和modCount是否相等。若不相等，就会排除ConcurrentModificationException异常，从而产生fail-fast情况。

expectedModCount的值定义为modCount，所以一旦初始化之后，就不会在被修改。而modCount的值，在集合元素数量变化的时候，都会被修改。所以在迭代的过程中，集合的元素数量一旦发生变化，就会产生fail-fast情况。

## fail-safe机制

* 定义：安全的错误
* 概念：在线程安全的集合中，迭代器是拷贝集合的副本进行迭代的，所以即使在迭代过程中修改原集合，也不会出现角标越界的情况。但相对的，会出现不符合预期的情况，此时迭代结果和原集合内容已经不一致。

为了避免fail-fast导致异常，我们可以使用Java中提供的一些采用fail-sale机制的集合。

这样的集合容器在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。

java.util.concurrent包下的容器都是fail-safe的，可以在多线程下并发使用，并发修改。同时也可以在foreach中进行add/remove。

以 CopyOnWriteList 为例，分析fail-safe机制：

![CopyOnWriteArrayList迭代器1](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/CopyOnWirteArrayList_001.png)
![CopyOnWriteArrayList迭代器2](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/CopyOnWriteArrayList_002.png)

从上图的源码中，可以得知

fail-safe集合的所有对集合的修改都是先拷贝一份副本，然后在副本集合上进行的。CopyOnWriteArrayList中的迭代器在迭代的过程中并不需要做fail-fast的并发检测。

迭代器是在迭代集合副本，所以集合在迭代期间发生的变化，迭代器是不知道的。

Copy-On-Write

在了解了CopyOnWriteArrayList之后，不知道大家会不会有这样的疑问：他的add/remove等方法都已经加锁了，还要copy一份再修改干嘛？多此一举？同样是线程安全的集合，这玩意和Vector有啥区别呢？

Copy-On-Write简称COW，是一种用于程序设计中的优化策略。其基本思路是，从一开始大家都在共享同一个内容，当某个人想要修改这个内容的时候，才会真正把内容Copy出去形成一个新的内容然后再改，这是一种延时懒惰策略。

CopyOnWrite容器即写时复制的容器。通俗的理解是当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容器进行Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素之后，再将原容器的引用指向新的容器。

CopyOnWriteArrayList中add/remove等写方法是需要加锁的，目的是为了避免Copy出N个副本出来，导致并发写。

但是，CopyOnWriteArrayList中的读方法是没有加锁的。

```
public E get(int index) {
    return get(getArray(), index);
}
```

这样做的好处是我们可以对CopyOnWrite容器进行并发的读，当然，这里读到的数据可能不是最新的。因为写时复制的思想是通过延时更新的策略来实现数据的最终一致性的，并非强一致性。

所以CopyOnWrite容器是一种读写分离的思想，读和写不同的容器。而Vector在读写的时候使用同一个容器，读写互斥，同时只能做一件事儿。

![CopyOnWriteArrayList的add()](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/CopyOnWriteArrayList_03.png)

## 参考
* [Java中的fail-fast机制](https://www.hollischuang.com/archives/33)
* [Java中的增强for循环（for each）的实现原理与坑](https://www.hollischuang.com/archives/1776)
* [一不小心就踩坑的fail-fast是个什么鬼？](https://www.hollischuang.com/archives/3542>)

