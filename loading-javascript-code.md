## Introduction

While Aurelia is very easy to understand from a sufficiently high level of abstraction: a framework for extending HTML using JavaScript, where the whole application built with Aurelia consists of Aurelia "components", defined as view (HTML) and view model (JS) pairs, which are nicely bound together - as stated in **[Aurelia Documentation](http://aurelia.io/docs.html#views-and-view-models)**:

>In Aurelia, user interface elements are composed of view and view-model pairs. The view is written with HTML and is rendered into the DOM. The view-model is written with JavaScript and provides data and behavior to the view. The templating engine and/or DI are responsible for creating these pairs and enforcing a predictable lifecycle for the process. Once instantiated, Aurelia's powerful databinding links the two pieces together allowing changes in your data to be reflected in the view and vice versa. This Separation of Concerns is great for developer/designer collaboration, maintainability, architectural flexibility, and even source control.

There is a snag however, which shows the moment you dive into the details:

- Organizing Aurelia code into modules
- How to load the Aurelia code (modules)
- How to access the existing (third party) code

These problems are not really new in any JavaScript development context - however, Aurelia being the most forward looking JavaScript framework internally uses ECMAScript 6 and ECMAScript 7 (see **[this](http://www.2ality.com/2011/09/es6-8.html)** for more details), resulting with a lot more complex environment than most JavaScript developers are used to. 

This article presents the brief history of JavaScript loading and the the recipes for using the tools like jpms, systemjs in the context of creating the needed Aurelia run-time context. As such this article is really just a compilation of well known methods and processes presented in the proper order with sufficient details


----------

----------
