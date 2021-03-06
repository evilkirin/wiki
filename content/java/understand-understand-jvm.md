---
title: "Try to understand 'Understand JVM'"
date: 2016-03-27 12:11
---

这是我第一次真正意义上的尝试将“深入理解Java虚拟机”读薄，因为我以前只会囫囵吞枣，只会抓起来一本书就看，不知道理解，不知道总结。我一开始也想尝试[How to Read a Book a Week](https://hbr.org/2016/02/how-to-read-a-book-a-week)这样去读，但是我发现这本书细节太多，以至于有些东西我还觉得作者讲的不够清楚。因此，略读并非一个好的办法。

我没法在阅读的速度上变快，我只能尝试着用一些办法让自己理解得更快，更快地将信息转化为知识，以更好地支撑自己的工作。比如，积累足够多的疑问，又比如时刻保持一个大局观。当然，也不是说前面那篇文章的东西在这里一点都用不上，但是我更需要的是[The ultimate guide to learning anything faster](http://thenextweb.com/lifehacks/2015/06/07/the-ultimate-guide-to-learning-anything-faster/)。

# 第二部分 自动内存管理机制

## 第2章 Java内存区域与内存溢出异常

### 概述：笔者将从概念上介绍Java虚拟机内存的各个区域，讲解这些区域的作用、服务对象以及其中可能产生的问题，这是翻越虚拟机内存管理这堵围墙的第一步。

### 本章小结：通过本章的学习，我们明白了虚拟机中的内存是如何划分的，那部分区域、什么样的代码和操作会导致内存溢出异常。虽然Java有垃圾收集机制，但内存溢出异常离我们仍然并不遥远，本章知识讲解了各个区域出现内存溢出异常的原因，第3章将详细讲解Java垃圾收集机制为了避免内存溢出异常的出现都做了哪些努力。

#### 运行时数据区

首先讲了JVM中运行时数据区的组成部分：程序计数器、虚拟机栈、本地方法栈、方法区、方法区中的常量池、堆，以及堆外内存也就是直接内存。

针对这部分可以有以下问题：
1. 既然是数据区，划分出来的这些区域主要存储些什么数据？生命周期有什么特点？
2. 这些不同的数据都会被谁在什么情况下使用？哪些是线程共享的，哪些是线程独有的？

#### Java堆

然后把堆给拎了出来，我们平时编程使用的最多的对象就存储在这里（暂时不考虑直接内存）。在三个方面针对对象进行了探讨：对象如何创建、对象如何存储以及对象如何访问。

问题如下：
1. JVM在收到一条new指令之后，都做了些什么事情来创建一个可用的对象？（根据参数找到一个类的符号引用确定对应的类是否已经加载、解析并完成初始化，然后通过bump-the-pointor或者free-list找到一块足够大的区域，赋值0，再以这块区域的引用作为this执行constructor。考虑到线程安全的问题，还需要考虑是否使用TLAB）
2. 对象如何在内存中如何布局的？
3. JVM如何定位一个即将被使用的对象？具体的数据字段如何摆放？

文中没有完全讲清楚的问题:
1. 为了提升数据利用率，降低元数据存储的overhead，Mark Word会被重用。Mark Word在未锁定状态下保存的内容：对象hash什么会被用到？Mark Word转换到其他状态后这部分数据跑到哪儿去了？
2. 采用直接指针访问策略时，reference在GC时是如何修改？

#### 各个数据区所服务的对象

最后验证了各个区域存储的数据，并演示了这些区域存储数据超出设置时会出现什么情况。其实就是各种溢出。。

## 第3章 垃圾收集器与内存分配策略

从这一章可以明显看出，大部分功能点都是事出有因，并非凭空蹦出来的。把事情的来龙去脉搞清楚对理解的帮助很大。

### 概述：为什么我们要去了解GC和内存分配呢？答案很简单：当需要排查各种内存溢出、内存泄漏问题时，当垃圾收集成为系统达到更高并发量的瓶颈时，我们就需要对这些“自动化”的技术实施必要的监控和调节。GC需要完成三件事情：哪些内存需要回收？什么时候回收？如何回收？

程序计数器、虚拟机栈和本地方法栈这三个区域随线程而生，随线程而灭；栈中的栈帧随着方法的进入和退出而有条不紊地执行者入栈和出栈操作，并且每个栈帧中分配多少内存基本上是在类结构确定下来时就已知的。而Java堆和方法区则不一样，垃圾收集器所关注的也就是这部分内存。

### 本章小结：本章介绍了垃圾收集的算法、几款JDK1.7中提供的垃圾收集器的特点以及运作原理。通过代码实例验证了Java虚拟机中自动内存分配及回收的主要规则。

#### 废弃对象标记算法 What

首先讲的是如何判断对象应该被回收了，也就是哪些内存需要回收。包括最基础的引用计数法和实际使用的可达性分析算法。可达性算法基本上就是拿到一个对象列表，然后从GC Roots开始搜索并生成一个引用链，列表中哪些对象没有在出现在引用链中即是可被回收的对象。

因为这两种算法都是依赖于对象的引用来做判断，作者在这里也讨论了一下JDK1.2中对引用概念的扩充：强引用、软引用、弱引用和虚引用。最后，以方法区中废弃常量和无用的类的回收结束了这个小节。

问题：
1. 有了标记算法，各个内存区域究竟是如何进行扫描的？其实只有堆和方法区才会进行回收。
2. GC Roots都有哪些？

#### 垃圾回收算法 How

接下来讲的是几种垃圾回收算法，它们都是以前一个小节中讲的可达性分析作为基础，先标记垃圾对象，然后执行不同的操作来扩大可用的内存区域。包括了：清除、复制、整理几种方法。分代是针对对象存活周期的不同将内存划分为几块，不同的区域使用不同的算法。

[Tuning the Java Heap (Sun Java System Application Server Enterprise Edition 8.2 Performance Tuning Guide)](https://docs.oracle.com/cd/E19900-01/819-4742/6n6sfgml5/index.html)里边提到，new和tenure的default ratio是1:2。

问题：
1. 为什么新生代用复制而老年代用整理算法？
2. 新生代实际使用的复制算法有什么特点？

#### HotSpot实现垃圾回收算法的几个要点 How exactly

为了提升性能，Hotspot在实现上述垃圾收集算法时，使用了一些特殊的技术来提升算法的执行效率。这一节主要讲的是Hotspot如何发起内存的回收。其中最关键的是OopMap、安全点和安全区域。

#### 垃圾收集器 Implementation

既然讲了发起，就要将如何执行。内存回收如何执行时由虚拟机所采用的GC收集器决定的，通常虚拟机中也往往不止有一种GC收集器。

Serial可搭配SerialOld和CMS使用，ParNew可搭配SerialOld和CMS使用，Parallel Scavenge可搭配SerialOld和Parallel Old使用。

在讲完了几种垃圾收集器之后，作者还介绍了一下GC日志，以参数总结结束本节。

问题：
1. CMS有哪些缺点？
2. CMS与SerialOld有什么样的联系？-XX:CMSInitiatingOccupancyFraction是个什么参数？
3. CMS和PS收集器分别的侧重点是什么？
4. 如果新生代的对象被老年代的对象引用怎么办？
5. G1名称的由来

#### 内存分配与回收策略

分配规则大体相同，细切取决于当前使用的是哪一种垃圾收集器组合，还有虚拟机中与内存相关的参数。

作者总结了几条最普遍的内存分配规则：
1. 对象优先在Eden分配
2. 大对象直接进入老年代 -XX:PretenureSizeThreshold
3. 长期存活的对象将进入老年代 -XX:MaxTenuringThreshold
4. 动态对象年龄判断 
5. 空间分配担保 -XX:HandlePromotionFailure

问题：
1. 内存分配的基本策略是怎么样的？
2. HandlePromotionFailure这个参数的意义是什么，在JDK6Update24之后这个参数的功能有什么变化？
3. yong gc vs. major gc vs. full gc

#### Bonus

- [Java Garbage Collection handbook by @JavaPlumbr](https://plumbr.eu/java-garbage-collection-handbook)中对各个GC的实现进行了更详细的讲解，比对着GC Log来说明具体执行了哪些操作，日志的组成部分和含义。
- [JVM调优总结 -Xms -Xmx -Xmn -Xss - unixboy - ITeye技术网站](http://unixboy.iteye.com/blog/174173)，总结了所有常用的GC参数，也有比较简单的调优建议
- [Useful JVM Flags - Part 7 (CMS Collector) - codecentric Blog : codecentric Blog](https://blog.codecentric.de/en/2013/10/useful-jvm-flags-part-7-cms-collector/)给出了更为详尽的CMS控制参数

## 第4章 虚拟机性能监控与故障处理工具

这一章主要在介绍各种工具，都是非常有用的，多用几次就熟练了。

- jps
- jstat, JVM statistics monitoring tool
- jinfo, configuration info for Java
- jmap, memory ap for java
- jhat, JVM heap dump browser
- jstack


