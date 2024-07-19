---
layout: post
title: "How to Win a Hackathon"
date: 2020-09-06
description: "Tips from a 2-time SwampHacks winner"
giscus_comments: true
toc:
  sidebar: left
tag: programming
citation: true
---

Like many Computer Science (CS) students, I frequently attend hackathons. I encourage any CS student who has the opportunity to go. They are great places to develop new connections, learn new technologies, and complete resume-building projects. If your resume is already excellent, then company sponsors will have tables where you can meet and discuss job opportunities. There are games, swag, and free food.

The main event at a hackathon, however, is the hacking: you have 24/36/48 hours to complete a project, with the option to present at the end. Prizes are awarded by the event and companies to the best hacks. I have been fortunate enough to win at two events, [SwampHacks IV (2018)](http://2018.swamphacks.com/public/index.html) and [SwampHacks VI (2020)](https://2020.swamphacks.com/). Here is my advice.

## 1. Find a Diverse Team

Hackathons allow teams of up to 4 when submitting projects; your team should have at least 3 members. Judges do not take team size into consideration when evaluating presentations, and prizes are per person. More importantly, the skillset of each team member should be disjoint. There is no point having two web developers, mobile developers, or machine learning (ML) practitioners. Dividing tasks is difficult, especially when there is no existing structure. Doubling up on one skill means missing out on another crucial skills.

The best way to find a diverse team at a hackathon is to make one beforehand. However, it is definitely possible to build balanced teams during the event. Most hackathons use a Slack workspace to communicate, with a dedicated channel for team building. There will be requests for people with specific skills.

> At SwampHacks IV, a student from Miami made a post looking for someone with ML experience. After hearing his idea, I joined the team. He found an experienced mobile developer and another ML engineer from Slack.

## 2. Come Up With a Strong Concept

The most crucial element to winning any prize is the strength of your idea. There is no point building beautiful, sophisticated, fast application that provides no user benefit or duplicates an existing product. It is critical that the idea of your project is stronger than your execution. Judges are sympathetic to the fact that 24/36/48 hours is not enough time to build a fully realized application. They are much harsher on poorly conceived projects.

Spend at least a few hours thinking about your idea, but no more than 33% of the entire duration. Any later risks not having enough time to build anything meaningful. Use prizes as inspiration. If you need to tackle a specific problem, think of a technological solution. If there are technology requirements, think of what it might let you build. Your project should target several prizes to optimize your odds of winning.

> At SwampHacks VI, we targeted 3 prizes: Best Hack for Disaster Relief, Photography/Digital Image Challenge, and Best Use of Google Cloud. Our [project](https://devpost.com/software/dizviz) used Google Cloud ML to process disaster images from social media which would be combined into a VR environment for first responders using photogrammetry.

## 3. Build a Compelling Demo

While it is not necessary to build a fully flushed out demo, you should implement the core functionality. There should be enough features that judges can envision the production-ready application: how a user would interact with it, how it would convenience user's lives, how it could positively impact society. The demo should be impressive, flashy even.

> At SwampHacks IV, we built an [Android app](https://devpost.com/software/opendoors) that would buzz if the camera was pointed at a door. There was a noticeable delay between pointing the camera and the phone buzzing. The classification was only 70% reliable. However, it was easy to overlook these flaws. Judges even offered their own suggestions such as buzzing more frequently the closer the door.

The easiest way to attract attention are to include hyped technologies like VR/AR, machine learning, or blockchain. But stick to what you know. Learning a new language/framework/library takes time, which will not be in abundance. Ideally, you would attend a hackathon knowing how to

- create a simple web app using [React](https://reactjs.org/docs/create-a-new-react-app.html) and [NodeJS](https://expressjs.com/en/starter/hello-world.html)
- create an [iOS](https://developer.apple.com/tutorials/app-dev-training)/[Android](https://developer.android.com/training/basics/firstapp) mobile app
- train an image classifier using [PyTorch](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html)
- make a VR game using [Unity](https://developer.oculus.com/documentation/unity/unity-tutorial/?locale=en_US).

Covering these 4 cases should be sufficient to build 99% of concepts.

## 4. Tell a Story

Giving talks is more art than science and requires practice to master. I pull my advice from my research experience. Almost every paper writes in the following format.

$$
problem \longrightarrow solution
$$

Define the problem you are trying to solve. Why is it important? Why have previous solution attempts failed? Then introduce your solution. How does it solve the problem at hand? What opportunities are there for future improvement?

In my opinion, the presentation is the easiest step. If you have laid the groundwork by **Finding a Diverse Team**, **Come Up With a Strong Concept**, and **Built a Compelling Demo**, the presentation should naturally follow. At this point, you will have been designing, coding, and thinking for 2 days. You will be excited about what you have done. You will be jumping to share your project. Ultimately, presentations are a form of story telling. Hopefully, you have a good one to tell.
