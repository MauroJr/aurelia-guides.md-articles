## Introduction

Like many of my contemporaries, I missed the relevance of JavaScript completely. While I can find some really good excuses - like I was leading a team of world class developers creating the only independent (from Sun) implementation of Java, at the time Netscape introduced JavaScript for the first time (it was named Mocha at that time - see **[this article](https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript)** for more details). Few months later the name was changed to **LiveScript** signalling its intent to be used to make the websites more "alive" - and we **real Java hackers** despised it from the very start. 

Now, twenty years later JavaScript fulfills the old dream of distributed application developers - running the same code on the client and the server side, thanks to **[V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine))** project and that alone warrants all of the retraining the people who missed JavaScript like me have to go through.

Today, the term JavaScript still references the ECMA-262 5th edition published in December 2009, probably best explained in David Flanagan's book JavaScript, The Definitive Guide (with sub-title "Activate your web pages"). While it took me a long time to get used to write code in **that** JavaScript dialect, once written the application looked "wobbly" and incredibly difficult to debug and maintain.

Finding Aurelia which requires the use of ES6 / ES7 or TypeScript made all the difference in the world for me. Suddenly I felt in a "sane" environment again - like XAML / C# world I really liked, but the jump from comfortable coding practices to the today's **[standard Aurelia application skeleton](https://github.com/aurelia/skeleton-navigation)** was WAY too steep. 

----

## Starting really small (relatively speaking)

In order to help late-comers to the party, I decided to write a series of tutorials, starting with the **[simplest](http://blog.aurelia-guides.com/2015/08/22/smallest-aurelia-application-created-from-scratch/)** possible Aurelia application consisting just from two files presenting the ``view-model`` (app.js) and the ``view`` (app.html)

**app.js** 

    export class App {

    	constructor() {
    		this.message = "";
    	}

    	activate() {
    		this.message = 'hello world';
    	}	
      
    }

**app.html**

    <template>
      ${message}
    </template>

Note that the ``view-model`` is created as an **ES6** class and that the ``view`` is a **[HTML5 template](http://www.html5rocks.com/en/tutorials/webcomponents/template/)**

I wrote that this simplest app consists of just two files - the correct version of this statement requires the mention of the all other "stuff" (configuration files and all thousands of modules that all together can be described as "runtime") - shown below

![](http://i.imgur.com/1CITSO0.png)

Continue reading **[here](http://blog.aurelia-guides.com/2015/08/22/smallest-aurelia-application-created-from-scratch/)** to get the detailed understanding of how to create this minimalistic application.

----

## What is at the end of this tutorial?

Well, the end if very far as I want to evolve the initial step which introduced just the smallest possible **front end** of a web application to a fully fledged Line of Business web application - [defined](http://searchcio.techtarget.com/definition/LOB) as:

> An LOB application is one of the set of critical computer applications that are vital to running an enterprise. LOB applications are usually large programs that contain a number of integrated capabilities and tie into databases and database management systems.

For this tutorial, I selected the well regarded application developed by Congral, LLC code-named **Fairhaven**. This application handles all aspects of ***Management of Care*** - workflow assisted process that assists patients released to home based recovery after a treatment in the hospital. 

Until Fairhaven application got introduced, the process of releasing the patient started with someone pushing a paper document shown below into the hands of a pretty confused and groggy patient:

![](http://i.imgur.com/iLHhS1y.png)

The actual patient's compliance with the prescribed behavior in this "discharge letter" was left to the patient's family to ensure 

With Fairhaven app process starts by the ***Care Manager*** (a person with the skills of a nurse) selecting the patient to be discharged:

![](http://i.imgur.com/XFRpgeJ.png)

followed by creation of the workflow program that actually creates a series of requests to the patient, request that are equivalent to the instructions in the discharge in the form of a machine executable Care Managent Program (CMP):

![](http://i.imgur.com/tuMAfaY.png)

A typical daily encounter looks like this:

![](http://i.imgur.com/oUFW6ks.png)

where the Care Manager's view is

![](http://i.imgur.com/cOTbnqX.png)

----
----

## What was the middle one?

This title is the famous quote from **[Fish called Wanda](http://www.imdb.com/title/tt0095159/quotes)** one of my favorite movies of all time (it shows that I am a big fan of [Monty Python](https://en.wikipedia.org/wiki/Monty_Python). In our context here it hints that this segment should enumerate the all the steps that will be injected between the **[first](http://blog.aurelia-guides.com/2015/08/22/smallest-aurelia-application-created-from-scratch/)** and last introduced above).

----
----

#Summary

Fairhaven is a great example of a complex distributed web application, parts of which are running on a server (this original app was serving the needs of a large interstate hospital with thousands of patients) other parts running in the browser (this is the typical use case for Aurelia written front end) or any of the smart devices that will be supported by Aurelia. 

This tutorial will guide you through the whole process of the design and implementation of this application - where each tutorial part will focus on a few single aspects of the complete application and will be built "on top" of previously defined parts.









