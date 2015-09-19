## Introduction

The official [Aurelia Navigation Skeleton Application](https://github.com/aurelia/skeleton-navigation) defines not only the recommended style for composing an Aurelia application - it also presents the complete workflow for building this application. By **workflow for building** we mean the process that starts with a set of application source files, continues with fetching all needed npm / jspm packages that  provide the application's runtime, compiles ("transpiles" is the actual term in this context) the source files, links the transpiled files with the runtime components and finally provides the means to run this fully assembled applications

**Note:** we are using the terms "transpiles", "links" and "runs" to associate this application building workflow with better know C/C++ application development workflow (for folks that developed code before nodejs became the "obsession" by many)

The Aurelia Application Building (and running) workflow is defined [here](https://github.com/aurelia/skeleton-navigation#running-the-app) - we will just summarize it to make this article easier to follow

**Step 1** Assume that the application is defined as a bunch of source code files - the set below represents the smallest meaningful set
- ``src/app.html``
- ``src/app.js``
- ``src/main.js``
- ``index.html``
- ``package.json``

The application is "composed" with all runtime components by running 
```
npm install
jspm install
```

**Step 2**
At this point, the application is organized as a file based hierarchy shown below

> :

![](http://i.imgur.com/zD5nxbd.png) 



