---
title: "Readable code - Christin Gorman"
date: 2016-01-23 10:04
---

- [Readable code - and the long lost secret of how to achieve it](https://vimeo.com/49484333)

<iframe src="https://player.vimeo.com/video/49484333" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

这样的seminar总是能一石激起千层浪，内容简短而激进，评论和回复反而更精彩。

Christin Gorman的核心观点是"don't hide it away"，方法的什么细节都一目了然，那些重构方法，比如extract method实际上是把问题复杂化了。下面是10分钟视频内容的summary。

1. 大家经常抱怨代码很长，很难读懂，但是作为professional，你应该learn how to read it
2. 不要看到一个很长的方法，就抑制不住冲动去抽取方法，把它变成成一堆小方法，the "don' hide it" theory，instead，你应该去整理一下这个代码的结构，让它更易读

Christin Gorman在评论中也补充了一下自己的观点: __I'm not saying all our methods should be enormous. All I'm saying is that all our methods don't have to be tiny. We shouldn't extract til we drop. We should extract till it makes sense.__ and __My mission was - in 10 minutes - to get people to think abit about how they refactor. Not just blindly extract untill they drop.__

"extract-till-you-drop refactoring"是太过了，"Uncle Bob says you're not a professional unless your methods are 5 lines long"更是比较极端，什么事情都还是需要要讲究一个度。

我觉得，不同的人有不同的品味，有不同的习惯和最舒服的读写代码的方式，最重要的是一个团队里边能够多多少少地达成一致，才能有更强的战斗力。

作为奇葩说的观众，这特别像是关于”是否应该讲一个大方法重构成更小的方法“的一场辩论”，相当有趣。

> Hightlights in comments
> 
> In fact, I regard a class with lots of private methods as a code smell of a possible violation of Single Responsibility Principle.
> 
> Much of the modern dogma just serves to make code hideous and unreadable.
> 
> In my opinion, such code is frequently a result of either blind following of "good practices" preached by Uncle Bob or someone else, or, also frequently, a failed attempt of refactoring, where the real problem, i.e. crappy incomprehensible algorithm/code is "fixed" by making the code look simple and neat, without actually simplifying it. For example, no doubt deep nesting has negative effect on comprehension, but so is replacement of this nesting with nested function calls. I would even argue that these nested calls are more difficult to understand than the original code.
> 
> As always applying a technique without understanding the motivation behind it will not gain you anything but headache.
> 
>  You should always try to be kind and consider other people that read your code even though you are too clever and knows everything well. A perfect readable code is much crafted by the understanding of your heart through years of experience and considering other people that will read your code.

更多层级的方法调用，应该会导致了解或理解the whole picture更困难，经验和能力水平是阅读和理解代码的关键因素。

> Most valuable comment & response IMHO
> 
> I've worked on many large projects with many developers and have never experienced a project that followed a 'x' lines of code rule. It would seem that Christin is preaching thinking which is a good thing. The problem is you need to gain a certain skill level to able to think. On large projects there is a tendency to try to control quality with rules instead of focusing on bring team member's skill level up.
I wonder if Christin considers her version of the code example as a method that does one thing? This is a difficult question because it is very subjective. Do you need a method that is the table contents when a method does several small things in the name of completing a task?
If everyone has a high skill level (not years of experience) then the code will read well no matter how it is written. The problem is on a large project they typically don't. I agree with Chrisitn that reading code is important, if fact, it may be the 'key' to rising skill level.

> Seems like you have got the message I was trying to convey. There are no silver bullets, we have to think about our current situation and write appropriate code. What "one thing" is will depend on the problems being solved. Some problems are easier to understand if you see more of the context in one go. Others are better off split up. Low skill levels will always be a problem no matter how large or small your units of code are. 
To improve your skills as a developer I would suggest
1) read and understand a lot of other peoples code
2) work on projects all by yourself - where you have to think up the solutions and then maintain them
3) work with others, pair programming etc, getting and giving feedback as often as possible
If I were a manager, I would try to ensure that all my employees get experience with all these 3 types of work.

Then comes the remark from Uncle Bob.

> It's quite good, short, energetic, enthusiastic, intelligent, and completely misses the point. 
While it's true that the code she produces is much better than the original, and is quite easy to understand; it fails one critical test. It's not polite.
Polite code is like a well written newspaper article. It allows you to bail out early. A well written article has a headline, a synopsis, and a set of paragraphs that begin with the high level concepts and get more and more detailed as you read through the article. At any point you can decide: "I get it! I don't need to read further." Indeed, this is how most people read newspapers or magazines.
The articles are polite, because they allow you to get out quickly.
Christin's code, simple as it is, does not let you get out early. You have to read through it to understand it. Granted, there's not a lot to read, and it's pretty easy going. But still, there's no early exit. To understand it, you must read it all.
Well written code should be crafted so that it is polite. It should approach detail gradually, the way a newspaper article does. It should allow the reader to bail out early, as soon as they realize that they don't need to understand the whole thing.

Response from Christin Gorman: [Impolite? Me? :-D - Objection](http://kranglefant.tumblr.com/post/31912613580/impolite-me-d)

> The best programmers don’t just follow guidelines (à la “extract til you drop”) blindly. The best programmers THINK for themselves.

现在看的代码规模随便就会上万行，所以读代码的方法也很重要，我自己的方案：
- 先做点准备工作，了解一下代码在做什么，需要什么，改变了什么
- 从弄懂主流程开始，从输入到输出，然后再分支路径

不过这也是针对一个code base，多个工程能够做个对比应当是更惬意的。


