---
layout: post
category: Best Practices / Clean Code Tips
tags: best practices, clean code, Robert Martin
title: Clean Code Tips (Week 1)
author: julianwaimann
---

Hello MakingSensers! Today I want to share the latest Clean Code Tips from the last week with you.

> * The name of a variable, function, or class should answer all the big questions. It should tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.

> * Programmers must avoid leaving false clues that obscure the meaning of code. We should avoid words whose entrenched meanings vary from our intended meaning. For example, hp, aix, and sco would be poor variable names. Abbreviations can be disinformative.

> * Avoid the “Do”, “Data”, “Work”, “Process”. These spawn strange creatures like “DoWork” “CheckData”, “ProcessEmployee” and other nameless horrors.

> * Noise words are redundant. The word variable should never appear in a variable name. The word table should never appear in a table name. How is NameString better than Name? Would a Name ever be a floating point number?

> * Classes and objects should have noun or noun phrase names like Customer, WikiPage,Account, and AddressParser. Methods should have verb or verb phrase names like postPayment, deletePage, or save.

> * Pick one word for one abstract concept and stick with it. For instance, it’s confusing to have “fetch”, “retrieve”,and “get” as equivalent methods of different classes.

> * People who read your code will be programmers. So, its a good idea to use computer science terms, algorithm names, pattern names, math terms, and so forth.

Special thanks to JD Raimondi, who added some new Clean Code ideas. Everybody is invited to share more tips.
All tips have been taken from Robert Martin’s Clean Code book

Stay tuned for the next week.