#Introduction

This article addresses one specific aspect of issues presented in **[What you need to know before writing your first Aurelia application](http://blog.aurelia-guides.com/2015/08/17/what-you-need-to-know-before-writing-your-first-aurelia-application/)** - what is **[jspm](http://jspm.io/)** and what is the relationship between **[Aurelia](http://aurelia.io/)** and **[jspm](http://jspm.io/)**.

----

### List of issues to cover

####1.
jspm's role is described as "Frictionless browser package management" - so I believe that it is important to start with the explanation that the JavaScript engine in the browser is different than the JavaScript engine in the NodeJS server (**[V8](https://code.google.com/p/v8/)**). This discussion also brings in **[Browserify](http://browserify.org/)**, which in turn benefits from **[Writing Modular JavaScript With AMD, CommonJS & ES Harmony](http://addyosmani.com/writing-modular-js/)** article.

####2.
Explain the jspm design which internally uses **[SystemJS](https://github.com/systemjs/systemjs)**, so it allows you to load any module system (AMD, CommonJS, ES6) and even use them interchangably in 1 app

####3.
Explain jspm's property to "understand" npm, (knows how to search npm's registry) and act as npm's proxy.

####4.
Explain **[jspm Registry](https://github.com/jspm/registry)**, the concept of "Package.json Overrides" and its role in Aurelia Developer's world.

####5.
Most of npm node packages are not fit to be used for Aurelia (for reasons explained in **Item 1.** above (difference between respective JavaScript engines) -- which is a big problem for JSPM users. Example:

    jspm install storpmath --save

This command will happily install the stormpath SDK which is written to run as a node application - and here we try to make ``Gulp`` use ``browserify`` to prepare this package to be loaded into the browser.
















