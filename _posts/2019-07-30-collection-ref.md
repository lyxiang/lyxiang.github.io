---
layout: post
title: Java中的集合关系
categories: Java 集合
keywords: Java 集合
---

Java 的所有集合类都位于 java.util 包，其中提供了一个表示和操作对象集合的统一构架，包含大量集合接口，以及这些接口的实现类和操作它们的算法。一个集合是一个对象，但它表示一组对象，Java 集合中实际存放的是对象的引用值，不能存放基本数据类型值。

---

## Collection接口

Collection是一个接口，所有的集合类(Map 除外)都要实现(或继承)该接口。Collection 接口提供了对集合进行基本操作的通用接口方法。

### Collection关系图
![Collection关系图](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/collection-ref.png)

## 集合工具类

### Collections

此类是由静态方法组合的工具类。包含对集合进行基本操作的方法

常用的方法:
* sort(List<T> list): 对list进行排序，默认升序
* sort(List<T> list, Comparator<? super T> c): 对list进行排序，按照c的规则排序

### Arrays

该类包含用于操作数组的各种方法（如排序和搜索）。 该类还包含一个静态工厂，可以将数组视为列表。

常用方法
* asList(T... a)：将数组转换为List集合。

## Map

Map<K,V> 集合类是将键映射到值。 Map 不能包含重复的键; 每个键可以映射到最多一个值。

Map 提供了一个更通用的元素存储方法。Map 集合类用于存储元素对（称作“键”和“值”），其中每个键映射到一个值。

### Map关系图
![Map关系图](https://raw.githubusercontent.com/lyxiang/lyxiang.github.io/master/images/blog/map-ref.png)
