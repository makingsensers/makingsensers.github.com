---
layout: post
title: Intro to MVVM
post_author: gclaret
author: gclaret
---

In this post, I want to share a very interesting presentation explaining the Model View ViewModel (MVVM) pattern, and how it can be implemented in WPF. After reading several blogs and web pages about this design pattern, I still couldn’t get my head around how it worked and it’s uses/advantages.

Then, I stumbled upon a post in which over 30 comments recommended a video on this topic by Jason Dollinger. I immediately decided to look it up, and give it a go. I must say, that hour and a half of presentation was far more productive than all the days I had spent on this topic!

What’s really good about this video, is that Jason starts out with a simple, yet powerful project example. He explains how to solve the problem in a more “traditional” way, with button clicks handled by event-handlers in the code behind, which then updated other parts of the UI. This is probably the approach that anyone without knowledge of WPF’s binding potential would take.

Here is where this gets interesting. After a lot of explanation about why this isn´t the way to do this, if you want to take full advantage of WPF, he starts to introduce the MVVM design concept. Using WPF, data binding and Commands, he transformed the application in a more manageable, readable and testable one.

A lot of other topics are covered in this video, such as Dependency Injection via Unity, Inversion of Control, Unit Testing, Blendability and much more. All of these concepts are really important to learn how to build a decoupled and testable application.

What’s really important about using this design patter, is that if you are building a robust application, with this separation of concerns, you can be working on all the logic of the code, while a designer is doing the View, totally oblivious of one another. Also, using mock ViewModels (also shown in the video), the designers can create test data to use in Blend, and see how it would look in dynamic data containers, such as GridViews.

After watching this presentation, I decided to watch it yet again, following the steps in his code, and recreate the application gradually. In this [GitHub repository](https://github.com/gclaret/WPF-Unleashed/tree/master/StockSubscriber/WpfApplication1), you can see this implementation. Keep in mind, that this was done in the same step-by-step fashion as the video, so in each commit, a new concept was introduced.

Also, if you are interested in downloading this video, it can be found [here](https://www.dropbox.com/s/7v2061ft6u67ikt/Jason_Dolinger_MVVM.wmv).

Check it out. It is, by far, the best introduction to MVVM and WPF I have found on the web!