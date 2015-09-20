## Introduction
Since the beginning of Aurelia days the **[Aurelia Skeleton Navigation Application](https://github.com/aurelia/skeleton-navigation)** is used as a start of almost any Aurelia project. At the same time there were many "newbie" questions in **[Aurelia Gitter chat room](https://gitter.im/Aurelia/Discuss)** about the details of this application's structure. 

So, Aurelia-Guides presents the process of building this application gradually from its basic components explaining all necessary details as we go along.

----------

## Tools we will use

- [Sublime 3](http://www.sublimetext.com/3) text editor
-  [Cmder](http://cmder.net/) console
- [Chrome](https://www.google.com/intl/en/chrome/browser/desktop/index.html#brand=CHMB&utm_campaign=en&utm_source=en-ha-na-us-sk&utm_medium=ha) browser
- [WebStorm](https://www.jetbrains.com/webstorm/) in all cases that require the server side debugging

**Note** See [Aurelia Development Environment and Tools](http://blog.aurelia-guides.com/2015/08/22/aurelia-development-environment-and-tools/#comment-33) and [What you need to know before writing your first Aurelia application](http://blog.aurelia-guides.com/2015/08/17/what-you-need-to-know-before-writing-your-first-aurelia-application/) for a more information 

-----

## Structure of the Aurelia Skeleton Navigation application

We are building the application which  will at the end have this **final** structure (shown is the version 0.18.1 being current at the time of writing this tutoria)l

![](http://i.imgur.com/Xn1J8jh.png)

-----

#### Let's start with the **smallest** meaningful subset of the application skeleton by following next 5 steps

### Step 1 

**Create the ``src`` folder and add the 4 minimally required files**

- ``app.html``  Application View

```html
<template>
  ${message}
</template>
```

- ``app.js``  Application View-Model

```javascript
export class App {

  constructor() {
    this.message = "";
  }

  activate() {
    this.message = 'hello world';
  }  
}
```

- ``main.js`` Application "entry-point"
 
```javascript
export function configure(aurelia) {
  aurelia.use
    .standardConfiguration()
    .developmentLogging();

  aurelia.start().then(a => a.setRoot());
}
```

- ``index.html``  This file should **not** be in the ``src`` folder - it should be located at the "root" level - sibling of the ``src`` folder

```html
<!doctype html>
<html>
  <head>
    <title>Aurelia Mini</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
  </head>
  <body aurelia-app="main">
    <h3>Loading...</h3>

    <script src="jspm_packages/system.js"></script>
    <script src="config.js"></script>
    <script>
      System.import('aurelia-bootstrapper');
    </script>
  </body>
</html>
```

This results with the complete set of source code files, where the **app.js** and **app.html** represent the very basic model / view model pair and the **main.js** file is defined as the application starting point (note the line `` <body aurelia-app="main">`` in the ``index.html``)

Next, note the two "key" lines in ``index.html``

```html
...
<script src="jspm_packages/system.js"></script>
<script src="config.js"></script>
...
```
which define the location where to get the [systemjs]() loader.

Lastly observe 
```html
<script>
      System.import('aurelia-bootstrapper');
</script>
``` 

telling the **[systemjs](https://github.com/systemjs/systemjs)** loader fetch and run ``aurelia-bootstrapper`` using the before mentioned ``main.js`` as the start of the execution. 

At this point our application skeleton is just this:

![](http://i.imgur.com/Xz91mHF.png)

### Step 2
 
**Add all runtime (system) components to our application**

It is the package.json file that defineds all "external" runtime components needeed by our application to able to run (in the context of the browser - you can find more details in the [Build - Debug - Deploy Workflow](https://github.com/aurelia-guides/aurelia-guides.md-articles/blob/master/Build-Debug-Deploy-Workflow.md) article). In order to keep this tutorial reasonably short, we will use the package.json that defines all packages needed by this skeleton application in its final state; most of these packages are not needed at this time when our application just shows the string "hello world!" on the screen.

Once the content of the package.json is defined, adding all runtime components is done by the two consecutive commands

```
npm install
jspm install
``` 

Running the first command takes several minutes (dependent on your computer) and it may emit hundreds of red warning lines caused by the absence of correct set of Microsoft's C++ DLLs used to compile parts of npm modules if you are using Windows as your development environment. None of these messages are fatal, as you will still be able to use JavaScript versions of those components that failed to compile.

The second line ``jspm install`` invokes the [jspm package manager](http://jspm.io/) which is a layer on top of npm and which will fetch all Aurelia Framework components and their direct dependencies. After this step, the project structure grew to be this:

![](http://i.imgur.com/cjaYJOe.png)

### Step 3
 
**Compile (build) our application**

Again, you can find more details of this step  in the [Build - Debug - Deploy Workflow](https://github.com/aurelia-guides/aurelia-guides.md-articles/blob/master/Build-Debug-Deploy-Workflow.md) article. Here we will just summarize the process that this step requires.

- **Add the ``build`` folder at the application root level, with the content shown below**:

![](http://i.imgur.com/rH7siUt.png)

The javascript files in the tasks folder are **[Gulp](http://gulpjs.com/)** scriptfiles - see **[this](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)** for details. Just to "show-off", here is the build.js script:

```javascript
var gulp = require('gulp');
var runSequence = require('run-sequence');
var changed = require('gulp-changed');
var plumber = require('gulp-plumber');
var to5 = require('gulp-babel');
var sourcemaps = require('gulp-sourcemaps');
var paths = require('../paths');
var compilerOptions = require('../babel-options');
var assign = Object.assign || require('object.assign');
var notify = require("gulp-notify");

// transpiles changed es6 files to SystemJS format
// the plumber() call prevents 'pipe breaking' caused
// by errors from other gulp plugins
// https://www.npmjs.com/package/gulp-plumber
gulp.task('build-system', function () {
  return gulp.src(paths.source)
    .pipe(plumber({errorHandler: notify.onError("Error: <%= error.message %>")}))
    .pipe(changed(paths.output, {extension: '.js'}))
    .pipe(sourcemaps.init({loadMaps: true}))
    .pipe(to5(assign({}, compilerOptions, {modules:'system'})))
    .pipe(sourcemaps.write({includeContent: true}))
    .pipe(gulp.dest(paths.output));
});

// copies changed html files to the output directory
gulp.task('build-html', function () {
  return gulp.src(paths.html)
    .pipe(changed(paths.output, {extension: '.html'}))
    .pipe(gulp.dest(paths.output));
});

// copies changed css files to the output directory
gulp.task('build-css', function () {
  return gulp.src(paths.css)
    .pipe(changed(paths.output, {extension: '.css'}))
    .pipe(gulp.dest(paths.output));
});

// this task calls the clean task (located
// in ./clean.js), then runs the build-system
// and build-html tasks in parallel
// https://www.npmjs.com/package/gulp-run-sequence
gulp.task('build', function(callback) {
  return runSequence(
    'clean',
    ['build-system', 'build-html', 'build-css'],
    callback
  );
});

```

- **Add the ``dist`` folder which will contain the output of the build step**


- **Add the ``gulpfile.js`` file  with the following content**
- 
```javascript
// all gulp tasks are located in the ./build/tasks directory
// gulp configuration is in files in ./build directory
require('require-dir')('build/tasks');
```

At this point we can issue ``gulp build`` command which will result with:

```
[17:54:14] Using gulpfile C:\work\Aurelia-Guides\ag-samples\AG_Aurelia_Application_Skeleton\gulpfile.js
[17:54:14] Starting 'build'...
[17:54:14] Starting 'clean'...
[17:54:14] Finished 'clean' after 26 ms
[17:54:14] Starting 'build-system'...
[17:54:14] Starting 'build-html'...
[17:54:14] Starting 'build-css'...
[17:54:14] Finished 'build-css' after 7.84 ms
[17:54:14] Finished 'build-html' after 154 ms
[17:54:15] Finished 'build-system' after 237 ms
[17:54:15] Finished 'build' after 272 ms
```

as a consequence of this process of building, observe that the initially empty ``dist`` folder now contains the compiled versions of our source files. Indeed it is the term ``transpiled`` that shoud be used instead of compiled - see **[this](http://k33g.github.io/2015/05/02/ES6.html)** for more information.

In particular that our original ES6 app.js code 

```javascript
export class App {

  constructor() {
    this.message = "";
  }

  activate() {
    this.message = 'hello world';
  }  
}
```

got transpiled into

```javascript
System.register([], function (_export) {
  "use strict";

  var App;

  var _createClass = (function () { function defineProperties(target, props) { for (var i = 0; i < props.length; i++) { var descriptor = props[i]; descriptor.enumerable = descriptor.enumerable || false; descriptor.configurable = true; if ("value" in descriptor) descriptor.writable = true; Object.defineProperty(target, descriptor.key, descriptor); } } return function (Constructor, protoProps, staticProps) { if (protoProps) defineProperties(Constructor.prototype, protoProps); if (staticProps) defineProperties(Constructor, staticProps); return Constructor; }; })();

  function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError("Cannot call a class as a function"); } }

  return {
    setters: [],
    execute: function () {
      App = (function () {
        function App() {
          _classCallCheck(this, App);

          this.message = "";
        }

        _createClass(App, [{
          key: "activate",
          value: function activate() {
            this.message = 'hello world';
          }
        }]);

        return App;
      })();

      _export("App", App);
    }
  };
});
//# sourceMappingURL=data:application/json;base64,eyJ2ZXJzaW9uIjozLCJzb3VyY2VzIjpbImFwcC5qcyJdLCJuYW1lcyI6W10sIm1hcHBpbmdzIjoiOzs7TUFBYSxHQUFHOzs7Ozs7Ozs7QUFBSCxTQUFHO0FBRUgsaUJBRkEsR0FBRyxHQUVBO2dDQUZILEdBQUc7O0FBR1osY0FBSSxDQUFDLE9BQU8sR0FBRyxFQUFFLENBQUM7U0FDbkI7O3FCQUpVLEdBQUc7O2lCQU1OLG9CQUFHO0FBQ1QsZ0JBQUksQ0FBQyxPQUFPLEdBQUcsYUFBYSxDQUFDO1dBQzlCOzs7ZUFSVSxHQUFHIiwiZmlsZSI6ImFwcC5qcyIsInNvdXJjZXNDb250ZW50IjpbImV4cG9ydCBjbGFzcyBBcHAge1xyXG5cclxuICBjb25zdHJ1Y3RvcigpIHtcclxuICAgIHRoaXMubWVzc2FnZSA9IFwiXCI7XHJcbiAgfVxyXG5cclxuICBhY3RpdmF0ZSgpIHtcclxuICAgIHRoaXMubWVzc2FnZSA9ICdoZWxsbyB3b3JsZCc7XHJcbiAgfSAgXHJcbn0iXSwic291cmNlUm9vdCI6Ii9zb3VyY2UvIn0=
```

This is a small but a nice example of why are we using ES6 JavaScript syntax for Aurelia.

### Step 4
 
**Running our application**

At this point we have everything in place - as we need to execute the ``gulp serve`` command defined as

```javascript
var gulp = require('gulp');
var browserSync = require('browser-sync');

// this task utilizes the browsersync plugin
// to create a dev server instance
// at http://localhost:9000
gulp.task('serve', ['build'], function(done) {
  browserSync({
    open: false,
    port: 9000,
    server: {
      baseDir: ['.'],
      middleware: function (req, res, next) {
        res.setHeader('Access-Control-Allow-Origin', '*');
        next();
      }
    }
  }, done);
});
```

**Important** before running the app (with assistance from **[Browsersync](http://www.browsersync.io/)** tool (see the above defined ``gulp serve`` command, we need to modify the file config.js, created by the ``jspm install'' command we executed before in **Step 2**. Here is the modifed section of this file (the added lines highlighted)

**config.js**

![](http://i.imgur.com/U5tbAwg.png)

Running this (``gulp serve``) command results with

```
λ gulp serve
[18:14:15] Using gulpfile C:\work\Aurelia-Guides\ag-samples\AG_Aurelia_Application_Skeleton\gulpfile.js
[18:14:15] Starting 'build'...
[18:14:15] Starting 'clean'...
[18:14:15] Finished 'clean' after 634 ms
[18:14:15] Starting 'build-system'...
[18:14:15] Starting 'build-html'...
[18:14:15] Starting 'build-css'...
[18:14:15] Finished 'build-css' after 22 ms
[18:14:15] Finished 'build-html' after 41 ms
[18:14:15] Finished 'build-system' after 80 ms
[18:14:15] Finished 'build' after 725 ms
[18:14:15] Starting 'serve'...
[BS] Local URL: http://localhost:9000
[BS] External URL: http://192.168.2.53:9000
[BS] Serving files from: .
[18:14:21] Finished 'serve' after 5.08 s
```

When setting the url to ``http://localhost:9000`` we get the expected view:

![](http://i.imgur.com/pHOZBus.png)

----------

### Adding Navigation (menu bar)

The application we developed so far is nearly complete - it still misses the complete testing infrastructure, that will be addressed in a different article. Aside from that, adding more functionality to the application is relatively very easy, as all we need to do is to add more view / view model pairs and add them to the ``src`` folder which at this point has just three files:

![](http://i.imgur.com/Xz91mHF.png)

While in the general case we will make the content of the ``src`` folder a nested structure to separate files by functionality (or some other preferred way), we can add the basic support for navigation quite simply - since we already added Boostrap and Fonts Awesome files in the **Step 2** above (check the content of the  ``package.json`` file).

Here are the updated versions of the the original  four files, needed to implement navigation.:

**app.html**

```html
<template>
  <require from="nav-bar.html"></require>
  <require from="bootstrap/css/bootstrap.css"></require>

  <nav-bar router.bind="router"></nav-bar>

  <div class="page-host">
    <router-view></router-view>
  </div>
</template>
```

**app.js**

Instead of the trivial initial version of the app.js, where we simply defined the "hello world " string to be printed as the only functionality of the application, here we are defining the three navigation routes, that should (together with **app.html**) result with this menu bar:

![](http://i.imgur.com/AjCDDZb.png)
 
```javascript
export class App {
  configureRouter(config, router){
    config.title = 'Aurelia';
    config.map([
      { route: ['','welcome'],  name: 'welcome',      moduleId: 'welcome',      nav: true, title:'Welcome' },
      { route: 'users',         name: 'users',        moduleId: 'users',        nav: true, title:'Github Users' },
      { route: 'child-router',  name: 'child-router', moduleId: 'child-router', nav: true, title:'Child Router' }
    ]);

    this.router = router;
  }
}

```
**main.js** - stays as is no changes needed

**index.html**

Almost no changes here - we just added two lines that define the references to .css files we need:

- **font-awesome.min.css** which was added to the project in the **Step 2** above
- **styles/styles.css** -  copied from the [original Navigation Skeleton Application](https://github.com/aurelia/skeleton-navigation)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Aurelia</title>
    <link rel="stylesheet" href="jspm_packages/npm/font-awesome@4.4.0/css/font-awesome.min.css">
    <link rel="stylesheet" href="styles/styles.css">
    <meta name="viewport" content="width=device-width, initial-scale=1">
  </head>

  <body aurelia-app="main">

    <script src="jspm_packages/system.js"></script>
    <script src="config.js"></script>
    <script>
      System.import('aurelia-bootstrapper');
    </script>
  </body>
</html>

```

The rest of the files:
- blur-image.js
- child-router.html
- child-router.js
- users.html
- users.js
- welcome.html
- welcome.js

are copied from the [original Navigation Skeleton Application](https://github.com/aurelia/skeleton-navigation) as well, without changes.

Finally, run ``gulp serve`` command to see the familiar rendering of our app:



This concludes the tutorial





