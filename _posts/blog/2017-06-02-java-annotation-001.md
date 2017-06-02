---
layout: post
title: Java注解学习（一）、元注解
categories: JAVA 注解
description: 我们学习注解就必须能定义自己的注解，并使用注解，在定义自己的注解之前，我们就必须要了解Java为我们提供的元注解和相关定义注解的语法。
keywords: JAVA, 注解, Annotation
---

我们学习注解就必须能定义自己的注解，并使用注解，在定义自己的注解之前，我们就必须要了解Java为我们提供的元注解和相关定义注解的语法。

## 元注解
元注解（meta annotation）的作用就是负责注解其他注解。Java5.0定义了4个标准的元注解类型，它们被用来提供对其它注解类型作说明。

  Java5.0定义的元注解：
  - @Target
  - @Retention
  - @Documented
  - @Inherited

这些类型和它们所支持的类在java.lang.annotation包中可以找到。下面我们看一下每个元注解的作用和相应分参数的使用说明。

## @Target
 - 作用：用于描述注解的使用范围（即：被描述的注解可以用在什么地方）
 - 说明：@Target定义的注解所修饰的对象范围：根据@Target给定的值可被用于 packages、types（类、接口、枚举、Annotation类型）、类型成员（方法、构造方法、成员变量、枚举值）、方法参数和本地变量（如循环变量、catch参数）。
 - @Target取值(ElementType)有：
