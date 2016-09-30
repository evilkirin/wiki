---
title: "Best of 'How to become a web developer' website"
date: 2016-01-17 19:40
---

> If you know OO, learn a functional language. I recommend Haskell since there is no way to cheat, be warned, your brain might melt a little.
在我犯之前的错误的时候，是不是自己在骗自己呢？自以为自己知道，自己明白，其实不然。

- [How you can get ahead by focusing on principles and not technologies - Better Programmer](http://aestheticio.com/can-get-ahead-focusing-principles-technologies/)  50%
    - Why should you focus on principles and not technologies?
        - Since they share characteristics you can safely assume that they will also have some of the same problems in your web app.
        - The more you focus on the underlying similarities the larger head start you will have the next time something new comes along.
    - Some practical tips:
        - Which older technologies was this inspired by?
        - Which problems is it trying to solve?
        - Which other new technologies are also solving the same problems?
        - How are all these technologies similar?
        - How do they differ?
    - Just like `<list of old technologies> <new technology> is <main purpose they all have in common>. Unlike previous attempts <new technology> is <what it is trying to do differently> by <how it’s doing it differently>`.
    - 我想，自己做过的项目，自己犯过的错误，都应该像这样好好总结一下，as said about inspections in[吾日三省吾身](http://www.mifengtd.cn/articles/daily-self-reflection-iaidehua.html)，有些问题是需要反复问自己的
        - 如何建立反省系统
            - 首先要明白自己要反省哪些方面（习惯：要明确自己要养成哪些习惯）
            - 收集
            - 整理与反省
            - 回顾，我认为这是整个过程中必不可少的
- [Want to become a web developer? 10 questions you should ask yourself.](http://aestheticio.com/10-questions-developers-should-ask-themselves/)  **50%**
    - Is there a pattern here?
        - leads to discovering the underlying principles
        - To understand is to perceive patterns
    - How can I make this simpler?
    - How does it work like that?
    - Has someone done this before?
    - Who said it first?
    - Do I love what I’m doing?
    - Where else can I use this?
        - Logic will get you from A to Z; imagination will get you everywhere.
        - 想法才是最重要的
    - What did I fail at today?
    - How can we make this possible?
    - Who can I learn from?
- [5 More questions developers should be asking themselves - Better Programmer](http://aestheticio.com/5-questions-developers-asking/)
    - Am I learning the right thing?
    - How can I make this more transparent?
    - What is the return on effort?
    - Am I solving the right problem?
        - Speak up! You are more than a code typist, you are a problem solver.
    - Does anybody care?
        - If what you are building doesn’t make somebodies life better, gives them more time, saves them money, why are you doing it?
    - **Start today**
        - You don’t have to do it all at once though. Try this; find somebody you work with who is also on a mission to be the best they can be. Pick one question per week and commit to asking each other that question at least once a day. **Think about your answers, be honest, be better.**
    - I should submit a comment after one of those posts… some other day.
- [You Must Tame Complexity to Become a Better Programmer](http://aestheticio.com/become-a-better-programmer-tame-complexity/)
    - Why is complexity so dangerous?
        - To avoid a problem you must first understand the problem.
        - **The more complex a system is the harder it is to understand. The harder a system is to understand the more likely you are to introduce more unnecessary complexity.**
        - This is the reason complexity is so dangerous. Every other problem in software development is either a side effect of complexity or only a problem because of complexity.
    - How complexity impacts understanding
        - Complexity makes testing less effective
            - With testing you try to understand the code from the outside. You observe how the system behaves under certain conditions and make assumptions based on that.
        - Complexity makes informal reasoning more difficult
            - When using reasoning you try to understand the system from the inside. By using the extra information available you are able to form a more accurate understanding of the program.
    - The three main causes of complexity
        - State
        - Control Flow
        - Code Volumn
    - Secondary causes of complexity
        - list of them:
            - Duplicated code
            - Dead code (unused code)
            - Missing abstractions
            - Unnecessary abstraction
            - Poor modularity
            - Missing documentation
        - they can be summarized with three principles
            - Complexity breeds complexity
            - Simplicity is hard
            - Power corrupts
    - Simplicity is not optional
    - Your mission is to pursue simplicity at all costs.
- [Why your code is so hard to understand - Better Programmer](http://aestheticio.com/why-your-code-is-hard-to-understand/)
    - Problem #1, overly complex mental models.
    - Problem #2, poor translation of semantic models into code.
        - Your task in translating a semantic model into syntax is to try and leave as many clues as possible that will allow you to rebuild the semantic model when you come back at a later time. How do you do this?
            - Class structure and names
            - Variables, parameter and method names
            - Single Responsibility Principle
            - Appropriate comments
    - Problem #3, not enough chunking.
    - Problem #4, obscured usage.
    - Problem #5, no clear path between the different models
    - Problem #6, inventing algorithms
    - Conclusion
        - In the end it boils down to this: as a programmer your goal is to construct **the simplest possible semantic model** that would solve your problem. Translate that semantic model as closely as possible into a **syntactic model (code)** and provide **as many clues as possible** so that whomever looks at your code after you can re-create the same semantic model you originally had in mind.
        - Imagine you are leaving breadcrumbs behind you as you walk through the brightly lit forest of your code. Trust me, when you need to find your way back later on, that forest is going to seem dark and misty and foreboding.
- [Become a better programmer](http://aestheticio.com/become-better-programmer-learning-understand-code/) *
    - To understand code you have to build a **mental model**
    - Your mental model is built up of matches between **general** and **specific knowledge**.
        - Your mental model consists of the set of links between the general and specific knowledge you have that is relevant to this problem.
    - Your ability to understand code is dependent on three things:
        1. Knowledge – The building blocks to solve the problem
        2. Links – The glue between the building blocks
        3. Hypotheses – The tools by which you form the links
    1. You can gain more general knowledge
        - Language specific knowledge
        - Programming concepts
        - Domain knowledge
    2. You can get better at matching code to general knowledge
        - Learn to recognize code beacons
        - Learn the rules of discourse
    3. You can get better at forming and revising hypotheses
        - Use a systematic approach
        - Use an opportunistic approach 