---
layout: essay
type: essay
published: true
title: Meteor
date: 2017-10-26
labels:
  - Meteor
  - Blaze
  - Mongo
---

I never thought about request response cycle when browsing internet. Refreshing feed continuously to get the latest updates was part of browsing internet. The concept of meteor did blow my mind. Any update in the server pushed out to all the clients is revolutionary when it comes to real time application. Also a mini mongo in client browser up to date with all subscribed data is very interesting. In theory, client could run the app offline with data in mini mongo. While the concept of Meteor is revolutionary, it is not the best option for many website. I would not want my web page to refresh as I am halfway through an article just because there was a small change in page. It not a good solution for a small app either. On the other hand, if there is a need for real-time data that scales well, Meteor is a good solution.

Meteor is awesome but understanding meteor syntax was no easy task. Proficiency in meteor requires at knowledge of blaze, reactiveness, MongoDB, javascript and more. I got lost in maze of imports at the first glance of Meteor. After years of working with SQL database, NoSQL was a very foreign concept to me. I did not understand the point of a database that did not pass the ACID test. And the syntax of blaze just confused me. It took me a long time to understand that errorMessage=(fieldError “first”) was a call to fieldError function with first as the parameter and the return value assigned to errorMessage. Working through meteor whether it was digit or bowfolio, the first few hours was just taking notes of all the concepts that confused me. The plan was to come back to them when I had time to do a deep dive into those concepts.

ESLint, meteor console, meteor chrome extensions and chrome developer mode were great help as I played around with Meteor. However, tracking logical errors has been the biggest problem I have encountered so far. Modularity of meteor complicates troubleshooting logical errors. I didn’t know where to start troubleshooting when there were no syntactical errors. While modularity is giving me problems right now, I am sure modularity would have helped me troubleshooting those same issues if I had deeper understanding of Meteor. Modularity does take some time to get used to. With just superficial understanding, I have been able to mockup an app for work in just few hours. It is an app to checkout and return equipments. Using the pre-built form controls from digit app, it did not take too long to get eight pages of the webpage up and running. Meteor handles most of the heavy lifting of as long as you understand the layout and syntax.

Meteor is definitely not easy for a beginner but after couple of weeks of hacking on it, things did start making sense. Many of the questions I had in my notes started to look obvious. MongoDB does not look as foreign and I understand there is a place for light weight database that do not have acid properties. But the syntax still look weird.
