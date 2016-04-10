---
title: "This is the JavaCompiler you might not known"
date: 2016-03-27 12:11
---

为了让JVM能够运行你所编写的程序，我们所写的源代码要经过一长传的处理步骤，粗糙一点来讲至少可以分为编写、编译、加载和执行这四个步骤。JavaCompiler是执行编译这一步的关键，只有当它将源代码编译成字节码之后，Classloader才有机会去加载我们的代码。

在Java 1.6之后，JDK中提供了编程式访问JavaCompiler的API，这使得我们在代码中以一种标准的方式来动态编译Java源代码并使用编译所生成的类成为可能。一开始了解到这个东西是我在无意中发现了一个别人编写的Java REPL，我当时就想能不能让这个REPL具备直接使用HSF的能力呢。我确实也实现了这样一个东西，但是后来发现其实并没有太大的用处，工作中也不怎么能用的到，最后就没有继续开发下去。

不过这个过程让我真正明白了Classloader是在做什么，这个过程中也收集了一些Classloader的内容。

# JavaCompiler


