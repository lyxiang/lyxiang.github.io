---
layout: post
title: Autowired 和 Resource的区别
categories: Java Spring
keywords: Autowired Resource
---

@Autowired 和 @resource 两者都可以用来实现 bean 的注入。

---

@Autowired 是 Spring 的注解， org.springframework.beans.factory.annotation.Autowired。

@Resource 是 Java 自带的注解， javax.annotation.Resource。

@Autowired 是按照 byTepe 来注入的，需要按名字注入的话可以跟 @Qualifier 搭配使用

@Resource 是按照里面的 byName 来注入的

* byName: 通过Bean的id或者name
* byType: 通过 class="com.lyxiang.dao.impl.UserDaoImpl"

面向接口编程：

一个接口一个实现类的情况下，用 @Autowired 或者 @Resource 均可以。

一个接口，多个实现类，用 @Resource 注入，只要保证属性名称不同即可。

一个接口，多个实现类，用 @Autowired 注入，要结合 @Qualifier 使用。


```

public interface UserService {

    String queryName();

}


@Service
public class UserServiceImpl1 implements UserService {
    @Override
    public String queryName() {
        return null;
    }
}

@Service
public class UserServiceImpl2 implements UserService {
    @Override
    public String queryName() {
        return null;
    }
}

@Resource(name = "userServiceImpl1")
UserService userService1;

@Resource(name = "userServiceImpl2")
UserService userService2;

@Autowired
@Qualifier(value = "userServiceImpl1")
UserService userService;

```
