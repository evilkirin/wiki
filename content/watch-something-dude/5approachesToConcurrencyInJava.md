---
title: "5 approaches to concurrency in Java - Christin & Eivind"
date: 2016-10-16 16:38
---

# 5 approaches to concurrency in Java - Christin & Eivind

<iframe src="https://player.vimeo.com/video/182070294" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

This topic talks about 5 approaches or frameworks: AKKA, Vert.x, Hystrix, Quasar and j.u.c. But it never did what the speakers said it was gonna.

虽然并没有真正从任何一个方面对框架进行比较，演讲的内容还是有点意思的。AKKA和Vertx都是好早就听说过，还专门看过Vertx创始人对这个框架的介绍Topic，有点像是JVM中的Nodejs，而且框架的设计初衷还包含对polyglot的原生支持。

Quasar的核心Fiber，我在之前看另外一个框架[jetlang/core](https://github.com/jetlang/core)也看到过。当时不太理解，其实Fiber就是用户态线程，与coroutine都是工作在用户态的一种调度工具。当然，不同的框架中实现偏向肯定有所不同。

其实这些框架就有点像不同的并发范式，都可以用来解决系统资源利用率的问题。

## 题外

- 这些框架要么放弃了原有的线程模型，要么基于线程模型。但都是设计出了一种新的任务分发管理机制。
- 给别人介绍一种复杂的概念时，可以将一些内容简化抽象，并与生活中常见的事物做内壁，尽量不要引入新的概念。