---
title: "BTrace Related"
date: 2016-09-25 11:18
---

从上层概念，到底层实践。

# 动态追踪

- [动态追踪技术漫谈 –](http://openresty.org/posts/dynamic-tracing/)
    + "把整个生产系统本身看成是一个可以直接查询的“数据库”，我们直接从这个“数据库”里安全快捷地得到我们想要的信息，而且绝不留痕迹，绝不去采集我们不需要的信息。"

# 实践

- [Btrace入门到熟练小工完全指南 | 江南白衣](http://calvin1978.blogcn.com/articles/btrace1.html)
    + "BTrace是神器，每一个需要每天解决线上问题，但完全不用BTrace的Java工程师，都是可疑的"

# 解析

- [BTrace原理之 -- VM Attach API](http://ivanzhangwb.github.io/btrace-vm-attach-api/)
- [BTrace原理浅析 - 后端技术杂谈 | 飒然Hang](http://www.rowkey.me/blog/2016/09/20/btrace/)
    + Client(Java compile api + attach api) + Agent（脚本解析引擎 + ASM + JDK6 Instumentation） + Socket