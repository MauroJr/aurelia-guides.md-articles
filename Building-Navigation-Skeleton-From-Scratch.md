## Introduction
Since the beginning of Aurelia days the **[Aurelia Skeleton Navigation Application](https://github.com/aurelia/skeleton-navigation)** is used as a start of almost any Aurelia project. At the same time there were many "newbie" questions in **[Aurelia Gitter chat room](https://gitter.im/Aurelia/Discuss)** about the details of this application's structure. 

So, Aurelia-Guides presents the process of building this application gradually from its basic components explaining all necessary details as we go along.

----------

## Tools we will use

- [Sublime 3](http://www.sublimetext.com/3) text editor
-  [Cmder](http://cmder.net/) console
- [Chrome](https://www.google.com/intl/en/chrome/browser/desktop/index.html#brand=CHMB&utm_campaign=en&utm_source=en-ha-na-us-sk&utm_medium=ha) browser
- [WebStorm](https://www.jetbrains.com/webstorm/) in all cases that require the server side debugging

**Note** See [Aurelia Development Environment and Tools](http://blog.aurelia-guides.com/2015/08/22/aurelia-development-environment-and-tools/#comment-33) and [What you need to know before writing your first Aurelia application](http://blog.aurelia-guides.com/2015/08/17/what-you-need-to-know-before-writing-your-first-aurelia-application/) for a lot more information 

-----

## Structure of the Aurelia Skeleton Navigation application

We are building the application which  will have this **final** structure (this is the version 0.18.1 being current at the time of writing this tutorial

![](http://i.imgur.com/Xn1J8jh.png)


Let's start with the smallest meaningful subset of this hierarchy:

**1** Create the ``src`` folder and add the 4 minimally required files
- ``app.html``
- ``app.js``
- ``main.js``
- ``index.html``  This file should not be in the ``src`` folder - it should be located at the "root" level - same as ``src`` folder








