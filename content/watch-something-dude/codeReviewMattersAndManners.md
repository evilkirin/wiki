---
title: "Code Review, Matters and Manners - Trisha & Maria "
date: 2016-10-15 16:30
---

- [Code Review Matters and Manners: Maria Khalusova, Trisha Gee on Vimeo](https://vimeo.com/182087729)

<iframe src="https://player.vimeo.com/video/182087729" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

从一年之前就在做code review的事情，今年换老板之后倒也还在坚持。但是因为现在主要是一个人干一块儿新的业务，自己的代码主要是自己和新老板看，周围的人也没怎么在做review的事情，缺少了一点氛围。

后来，在review新业务代码的时候，有一部分没有review到，结果这部分就出问题了。虽然是一个小问题，但是心里也不太是滋味。好在业务处在拓展期，后果也只是出现了一部分脏数据（当时设计的库忘了加Unique约束，结果那个时候也跑出来捣乱）。加上第一次在自己主导的项目中将一部分代码交给团队里边其他同学来完成，效果也不是特别理想（后来觉得还不如自己加个班写一下），那段时间真的有点懵。

此Java Zone的主题由两个人合作完成，第一部分有点意思，主要讲我们究竟应该review什么，第二部分把一个一般不会太重视，但是实际上会引起major problem的点拿出来做了讨论。

下面是第一个话题的几个点：

- Code Review is Too Late For Design
    + Do it in advance, or as you go
- Understand what's important
    + Decide on priorities, apply consistently
    + Usability
        * Readability
        * Maintainability
        * Extensability
    + Functionality
        * Do it do what it supposed to?
        * Does it meet "non-functional" requirements?
            - performance
            - security
- Dont sweat the little things
    + Automate these checks

虽说确实不应该在review阶段再去讨论设计的合理性，但是Trisha列出来的几个设计要考虑的点倒是有借鉴意义。

- line level
    + Is the **code** in the **right place**?
    + Are the **data structures** that have been used appropriate?
    + Have opportunities for **code-reuse** been taken?
    + Is the code **overly-complex** or **over-engineered**?
    + Have **new dependencies** been introduced?
    + Is the code making **use of exsiting libraries**?
    + Is it **utilising new idioms** from language updates?
- bigger things
    + Does the new code **fit with** the overall **architecture**?
    + Does the new code follow the current **design practices**?
    + Which **design patterns** are used in new code? Are these appropriate?
    + Does the code follow **SOLID principles**, **Domain Driven Design**, etc.


