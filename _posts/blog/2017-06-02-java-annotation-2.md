---
layout: post
title: Java注解学习（二）、元注解
categories: JAVA 注解
description: 我们学习注解就必须能定义自己的注解，并使用注解，在定义自己的注解之前，我们就必须要了解Java为我们提供的元注解和相关定义注解的语法。
keywords: JAVA, 注解, Annotation
---

我们学习注解就必须能定义自己的注解，并使用注解，在定义自己的注解之前，我们就必须要了解Java为我们提供的元注解和相关定义注解的语法。

## 元注解
元注解（meta-annotation）的作用就是负责注解其他注解。Java5.0定义了4个标准的元注解类型，它们被用来提供对其它注解类型作说明。

  Java5.0定义的元注解：
  - @Target
  - @Retention
  - @Documented
  - @Inherited

这些类型和它们所支持的类在java.lang.annotation包中可以找到。下面我们看一下每个元注解的作用和相应分参数的使用说明。

## @Target
 - 作用：用于描述注解的使用范围（即：被描述的注解可以用在什么地方）
 - 说明：@Target定义所修饰的注解使用范围：根据@Target给定的值可被用于 packages、types（类、接口、枚举、Annotation类型）、类型成员（方法、构造方法、成员变量、枚举值）、方法参数和本地变量（如循环变量、catch参数）。
 - @Target取值(ElementType)有：
    - TYPE：用于描述类、接口(包括注解类型) 或enum声明
    - FIELD：用于描述域（包括枚举常量）
    - METHOD：用于描述方法
    - PARAMETER：用于描述参数
    - CONSTRUCTOR：用于描述构造函数
    - LOCAL_VARIABLE：用于描述局部变量
    - ANNOTATION_TYPE：用于注解类型描述
    - PACKAGE：用于包描述
    - TYPE_PARAMETER：用于类型参数描述
    - TYPE_USE：用于类型使用描述

注：当@Target未指定值时，新定义的注解可以使用在任何地方

## @Retention
 - 作用：表示需要在什么级别保存该注释信息，用于描述注解的生命周期（即：被描述的注解在什么范围内有效）
 - 说明：@Retention定义所修饰的注解存在的生命周期：某些Annotation仅出现在源代码中，编译后被丢弃；而另一些却被编译在class文件中；编译在class文件中的Annotation可能会被虚拟机忽略，而另一些在class被装载时将被读取（请注意并不影响class的执行，因为Annotation与class在使用上是被分离的）。使用@Retention可以对 Annotation的“生命周期”限制。
 - @Retention取值(RetentionPolicy)有：
    - SOURCE：在源文件中有效（即源文件保留）
    - CLASS：在class文件中有效（即class保留）
    - RUNTIME：在运行时有效（即运行时保留）

## @Documented
 - 作用：@Documented修饰的注解会被包含在javaapi中，因此可以被例如javadoc此类的工具文档化。Documented是一个标记注解，没有成员。

## @Inherited
 - 作用：@Inherited阐述了某个被标注的类型是被继承的。如果一个使用了@Inherited修饰的annotation类型被用于一个class，则这个annotation将被用于该class的子类。即允许子类集成父类的注解，@Inherited 元注解是一个标记注解。

## 自定义注解
使用@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口，由编译程序自动完成其他细节。在定义注解时，不能继承其他的注解或接口。@interface用来声明一个注解，其中的每一个方法实际上是声明了一个配置参数。方法的名称就是参数的名称，返回值类型就是参数的类型（返回值类型只能是基本类型、Class、String、enum）。可以通过default来声明参数的默认值。
 - 定义注解格式：
　　public @interface 注解名 {定义体}

 - 注解参数的可支持数据类型：

　　　　1. 所有基本数据类型（int,float,boolean,byte,double,char,long,short)
　　　　2. String类型
　　　　3. Class类型
　　　　4. enum类型
　　　　5. Annotation类型
　　　　6. 以上所有类型的数组

 - 注解类型里面的参数该设定:
　　1. 只能用public或默认(default)这两个访问权修饰.例如,String value();这里把方法设为defaul默认类型；　 　
　　2. 参数成员只能用基本类型byte,short,char,int,long,float,double,boolean八种基本数据类型和 String,Enum,Class,annotations等数据类型,以及这一些类型的数组.例如,String value();这里的参数成员就为String;　　
　　3. 如果只有一个参数成员,最好把参数名称设为"value",后加小括号.例:下面的例子FruitName注解就只有一个参数成员。

## 注解元素的默认值
注解元素必须有确定的值，要么在定义注解的默认值中指定，要么在使用注解时指定，非基本类型的注解元素的值不可为null。因此, 使用空字符串或0作为默认值是一种常用的做法。这个约束使得处理器很难表现一个元素的存在或缺失的状态，因为每个注解的声明中，所有元素都存在，并且都具有相应的值，为了绕开这个约束，我们只能定义一些特殊的值，例如空字符串或者负数，一次表示某个元素不存在，在定义注解时，这已经成为一个习惯用法。
