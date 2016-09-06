---
title: "Java 8: Interface with Default Methods"
date: 2016-09-07 12:11
---

在[Dynamic proxies once again](http://darkzach.com/readsomecode/2016/08/07/Dynamic-proxies-once-again.html)里边，第一次在比较真实或者说比较复杂的场景中见识了default method in interface。今天在回顾这部分内容的时候突然意识到，Interface with default method和Abstract Class实际上是有“重合”的地方，但是又说不太清（明显理解不够透彻）。于是乎Google了一把，把一些相关的信息组织总结如下。

但是all in all, use default method whenever possible.

> 引用的文字主要来自于文章最末所引用SO问题中的回答和评论。

首先，默认方法的主要使用场景是用来实现一些工具方法，这是其本身只能访问**当前或所扩展接口**中其他的方法所带来的限制。之前只能用interface with companion class来实现的功能，比如AbstractCollection，就可以直接在Collection中用默认方法来实现了。

> The constraint on the default method is that it can be implemented only in the terms of calls to other interface methods, with no reference to a particular implementation's state. So the main use case is higher-level and convenience methods.
> 
> Default methods have put an end to classic pattern of interface and a companion class that implements most or all of the methods in that interface. An example is Collection and AbstractCollection. Now we should implement the methods in the interface itself to provide default functionality. The classes which implement the interface has choice to override the methods or inherit the default implementation.
> 
> The good thing about this new feature is that, where before you were forced to use an abstract class for the convenience methods, thus constraining the implementor to single inheritance, now you can have a really clean design with just the interface and a minimum of implementation effort forced on the programmer.

其次，默认方法主要的设计初衷是为了在之前版本就存在的接口中添加方法，thus the so called 'interface evolution'.

```java
List<?> list = …;
list.forEach(…);
```

为了在接口中添加诸如`Collection.stream()`此类的工具方法,而又不会破坏之前对接口的实现，Java 8带来了默认方法。

> Conceptually, main purpose of defender methods is a backward compatibility after introduction of new features (as lambda-functions) in Java 8.
> 
> The benefit that default methods bring is that now it’s possible to add a new default method to the interface and it doesn’t break the implementations.
> 
> We’ll it is because interfaces are too tightly coupled with their implementation classes. i.e. it is not possible to add a method in interface without breaking the implementor class. Once you add a method in interface, all its implemented classes must declare method body of this new method.
> Since Java 8, things started getting ugly. A new feature Lambda was introduce which is cool. However it is not possible to use this feature in existing Java libraries such as java.util package. If you add a single method in interface List, it breaks everything. You need to add its implementation in every class that implements List interface. Imagine in real world how many custom classes would change.

同时，这使得一个functional interface也可以包含多个方法。

> Besides having the possibility of adding methods to the interface in future versions, there is the important point of allowing an interface to stay a functional interface even if it has more than one method.
> 
> A functional interface has only one non-default abstract method which can be implemented via a lambda expression. One example is the Predicate interface which has only one abstract method (test) while providing default methods for negating a Predicate or combining it with another Predicate. Without default methods these methods had to be provided in another utility class like the pre-Java 8 Collections class (as you don’t want to give up the possibility of lambda implementations for such an interface).

Last, but not the least, even the best! 让行为的多重集成成为了可能，当然，限制多多。

> (Less dangerous) multiple inheritance; I have the same implimentation of the same interface all over my program because the implimenting classes extend different parent classes. This is going to reduce all that duplication into a single default method
> 
> Java always had multiple inheritance of types. This extends that same mechanism to support multiple inheritance of behavior, while staying away from the very troublesome topic of multiple inheritance of state (which is where all the pain comes from.)   --- from Brian Goetz

## 这并不是说Abstract Class不好

Abstract Class可以有构造函数，可以有状态。关键是它主要用来构建继承体系（Inheritance Hierachy）的。

> And abstract classes are a normal type of inheritance, they are normal classes which are intended to be extended.
> 
> Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation.
> However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods.
> 
> Abstract class can define constructor. They are more structured and can have a state associated with them. While in contrast, default method can be implemented only in the terms of invoking other interface methods, with no reference to a particular implementation's state. Hence, both use for different purposes and choosing between two really depends on the scenario context.

## Refs

- [Purpose of Default or Defender methods in Java 8 - Stack Overflow](http://stackoverflow.com/questions/19998309/purpose-of-default-or-defender-methods-in-java-8)
- [Interface with default methods vs Abstract class in Java 8 - Stack Overflow](http://stackoverflow.com/questions/19998454/interface-with-default-methods-vs-abstract-class-in-java-8)
- [language design - Why is "final" not allowed in Java 8 interface methods? - Stack Overflow](http://stackoverflow.com/questions/23453287/why-is-final-not-allowed-in-java-8-interface-methods/23476994#23476994)
- [Default Methods (The Java™ Tutorials > Learning the Java Language > Interfaces and Inheritance)](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html)
    + 官方教程，自己感觉写的相当不错
- [Everything You Need To Know About Default Methods](http://blog.codefx.org/java/everything-about-default-methods/#Default-Methods-vs-Abstract-Classes)
    + 更为系统的一篇文章，有空回头来看看
