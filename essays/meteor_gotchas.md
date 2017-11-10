---
layout: essay
type: essay
published: true
title: Meteor Gotchas
date: 2017-10-19
labels:
  - Software Engineering
  - Meteor
---
 
Meteor has been an interesting experience so far. It is a nit-picky black box. If everything is perfectly aligned as recommended, it works like a charm. One little syntaxical error and everything goes haywire. 

Reading the error message was the most difficult part about meteor. The first few times I saw those error messages, they just looked giberish. I didn't touch most the files, those errors were pointing to. After a week I feel like I am starting to understand the basics or at least have an idea of where to start troubleshooting. I start looking from the top of the error message and continue going down until I come across a file that I was warking on. It then points to the line number of the error. Most of the time I did not know what to do with those messages but at leasrt I knew where to start. And I have started using chrome developer tools more and more which helps a lot with troubleshooting.

Templates were another confusing thing when I got started with meteor. Following the trails of import only to find event and onCreated method of template object was disheartening. Event is a method of template object and within events, many objects are defined. It was just so confusing. watching videos of meteor-app and meteor-form did help. However, the best understanding I had was when I broke something.

Tackling some piece of code at a time has helped and I found that constant testing and having git branch to reset everything helps a lot. The more I inderstand meteor the more I am liking it.
