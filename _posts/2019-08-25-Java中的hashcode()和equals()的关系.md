---
layout: post
title: Java中的hashcode()和equals()的关系
categories: Java
keywords: Java hashcode equals
---

hashcode() 和 equals() 是 Java 所有对象的父类 Object 的成员方法。

hashcode() 是 Object 的一个本地方法，返回一个 int 值。

equals() 是 利用 == 来判断两个对象是否相等，比较的是内存地址。 

---

如果两个对象相等，那么他们一定有相同的哈希值。

如果两个对象的哈希值相等，那么这两个对象有可能相等也有可能不相等。（需要再通过equals来判断）

## hashcode()
* Java 中的 hashCode 方法就是根据一定的规则将与对象相关的信息（比如对象的存储地址，对象的字段等）映射成一个数值，这个数值称作为散列值。
* hashCode 方法主要作用是为了配合基于散列的集合一起运行

## equals()
* equals() 是用来判断两个对象是否相等
* 底层实现也很简单，就是利用 == 来实现，比较的是两个对象的内存地址

```
    public boolean equals(Object obj) {
        return (this == obj);
    }
```

## 重写equals就一定要重写hashCode吗

### 是的

当我们需要将对象存放入某些数据结构中时，例如HashMap，这时候当我们重写了equals就必须重写hashCode了。
在散列对象中，会优先使用对象的哈希值判断容器中是否存在该对象。当哈希值相同的时候，再结合 equals() 判断。

### 不是的
当我们只是单纯的使用 equals()，压根不会使用哈希值时，当然不用去重写 hashcode()。

## 本地方法
* Native Method：该方法的实现由非java语言实现，比如C。这个特征并非java所特有，很多其它的编程语言都有这一机制，比如在C＋＋中，你可以用extern "C"告知C＋＋编译器去调用一个C的函数。
* 定义一个 native method 时，并不提供实现体（有些像定义一个java interface），因为其实现体是由非 java 语言在外面实现的。