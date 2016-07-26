---
title: "SOLID, Object-Oriented Design - By Sandi Metz"
date: 2016-07-23 20:30
---

- [2009 - Sandi Metz - SOLID Object-Oriented Design on Vimeo](https://vimeo.com/12350535)

<iframe src="https://player.vimeo.com/video/12350535" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

> Your application will change.
> How’s that gonna work out for you.
> presentation: http://skmetz.home.mindspring.com/img1.html

- If testing seems hard - examine your design
- TDD will punish you if you don’t understand design

Questions to ask when trying to refactor:

- Is it DRY?
- Does it have one responsibility?
- Does everything in it change at the same rate?
- Does it depend on things that change less often than itself?

What am I trying to do when refactoring? Keep an eye on it. It seems I just try to find some appropriate patterns to apply. May be some TDD will be better.