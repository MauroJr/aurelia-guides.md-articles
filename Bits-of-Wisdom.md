## Summary

This page is a collection of brief explanations / advices of lot less depth than you could find at <http://blog.durandal.io/2015/02/03/aurelia-qa/> for example. This comes as the consequence that Aurelia Guides is the resource written by Aurelia Developers for Aurelia Developers and its purpose is to **augment** -- **not replace** [Aurelia official documentation][1].

* * *
* * *


## 1\. jspm package manager fails to find the npm module I need.

**Context Section**
Aurelia requires the use of **jspm** (see **[this](http://blog.aurelia-guides.com/2015/08/28/aurelia-and-jspm/)** for more information) and jspm is designed to load any "package" from either jspm registry, github and npm registry. This short article describes some less than happy experience in pursuing that goal with a specific package from npm registry that I used a lot in my "Angular days".

* * * 

Few days back, I wanted to create a sample of an Aurelia application which uses **[Stormpath Authentication and Authorization services][2]** (this sample is a part of a larger **[Aurelia Security Services][3]** article still under development).

As I prefer to start "from scratch" in the "experiment phase", I took the approach described in the document [Smallest Aurelia Application - created from scratch][4]. **Knowing** that I need [Official Stormpath SDK for Node.js][5] library, distributed via **[npm][6]**, and knowing further that I have to use **[jspm][7]** (package manager for [System.js module loader][8]) to load a package from npm registry into the Aurelia **[ES6][9]** world, the thing to do is simple

1.  Create my "[Smallest Aurelia Application][4]".
2.  Run `jspm install stormpath`

Well, instead of getting my app configured to have the access to Stormpath module, I got this:

    λ jspm install stormpath
    
    warn Running jspm globally, it is advisable to locally install jspm via npm install jspm --save-dev.
    
    Package.json file does not exist, create it? [yes]:y
    Would you like jspm to prefix the jspm package.json properties under jspm? [yes]:y
    Enter server baseURL (public folder path) [./]:y
    Enter jspm packages folder [y\jspm_packages]:y
    Enter config file path [y\config.js]:y
    Configuration file y doesn&amp;#39;t exist, create it? [yes]:
    Enter client baseURL (public folder URL) [/]:
    Do you wish to use an ES6 transpiler? [yes]:
    Which ES6 transpiler would you like to use, Babel or Traceur? [babel]:
         Updating registry cache...
    
    err  Repo jspm:stormpath not found!
    
    warn Installation changes not saved.
    
Does npm registry contain stormpath module? Yes, of course - as shown below
    
    λ npm install stormpath
    stormpath@0.10.2 node_modules\stormpath
    ├── njwt@0.0.1
    ├── jwt-simple@0.2.0
    ├── flat@1.6.0
    ├── deep-extend@0.4.0
    ├── underscore@1.5.2
    ├── async@0.7.0
    ├── node-uuid@1.4.3
    ├── redis@0.12.1
    ├── properties-parser@0.2.3
    ├── underscore.string@2.3.3
    ├── glob@3.2.11 (inherits@2.0.1, minimatch@0.3.0)
    ├── request@2.40.0 (forever-agent@0.5.2, aws-sign2@0.5.0, stringstream@0.0.4, oauth-sign@0.3.0, tunnel-agent@0.4.1, json-stringify-safe@5.0.1, qs@1.0.2, mime-types@1.0.2, form-data@0.1.4, http-signature@0.10.1, tough-cookie@2.0.0, hawk@1.1.1)
    ├── moment@2.8.4
    └── memcached@0.2.8 (hashring@0.0.8, jackpot@0.0.6)
    
Why did  my search for stormpath fail? Well, sometimes it is good to read the documentation **very carefully**. Had I done this, I would know that instead of  ``jspm install stormpath`` I should have written ``jspm install npm:stormpath``

* * *


## 2\. Should I write my apps using TypeScript or ES6?

**Context Section**
Aurelia applications can be written either in "plain" ES6 Javascript or TypeScript - and this question is often asked by many

 
See the **[answer][11]** provided by **Mike Graham**, introduced by **Rob Eisenberg**

* * *

After reading this blog post and being concerned about the all popular view that only TypeScript will prevent you from digging yourself a hole too deep to bail yourself out of - I asked Mike this same question in the context of "my app will be too big to be written JavaScript" issue.

"Stay with ES6 if you are comfortable with it" - was Mike's brief reply and I knew that he was pointing out that ES6 is a very different animal from today's ES5. So, at least for now, I am staying with ES6 :-)

----

## 3\. Use of jspm in Aurelia Skeleton-Navigation application

Aurelia Skeleton-Navigation application is often being used as the official definition of the internal application structure - at least at the beginning when not all utility tools like **[Aurelia cli](https://github.com/aurelia/cli)** are ready to be used. This article tries to reverse engineer the process of creating the Skeleton-Navigation application's config.json file

### Aurelia Skeleton-Navigation application packages from fetched by jspm

Note: packages from ``github/aurelia`` repository are omitted for clarity sake

    "jspm": {
      "dependencies": {
        ...
        "bootstrap": "github:twbs/bootstrap@^3.3.4",
        "clean-css": "npm:clean-css@^3.3.8",
        "core-js": "npm:core-js@^0.9.4",
        "css": "github:systemjs/plugin-css@^0.1.11",
        "fetch": "github:github/fetch@^0.9.0",
        "font-awesome": "npm:font-awesome@^4.3.0"
      },

####Issue 1:

 The author decided to request ``jspm`` to fetch the ``bootstrap`` package from [https://github.com/twbs](https://github.com/twbs) - **not from the npm registry** as one would expect and as it used to be recently - the [Bootstrap getting started](http://getbootstrap.com/getting-started/) document still claims that ``npm`` is the way to go.

Indeed, bootstrap package cannot be installed directly via ``npm`` or ``bower``

    npm WARN package.json test@1.0.0 No description
	npm WARN package.json test@1.0.0 No repository field.
	npm WARN package.json test@1.0.0 No README data
	npm ERR! Windows_NT 6.3.9600
	npm ERR! argv "C:\\Program Files\\nodejs\\\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "boostrap"
	npm ERR! node v0.12.5
	npm ERR! npm  v2.11.2
	npm ERR! code E404

	npm ERR! 404 Registry returned 404 for GET on https://registry.npmjs.org/boostrap
	npm ERR! 404
	npm ERR! 404 'boostrap' is not in the npm registry.
	npm ERR! 404 You should bug the author to publish it (or use the name yourself!)
	npm ERR! 404 It was specified as a dependency of 'test'
	npm ERR! 404
	npm ERR! 404 Note that you can also install from a
	npm ERR! 404 tarball, folder, http url, or git url.

	npm ERR! Please include the following file with any support request:
	npm ERR!     C:\Users\Nikolaj\test\npm-debug.log

----

####Issue 2:

The situation with  ``fetch`` module is different - it exists in npm registry (version 0.3.6):

    λ npm install fetch                                        
    npm WARN package.json test@1.0.0 No description            
    npm WARN package.json test@1.0.0 No repository field.      
    npm WARN package.json test@1.0.0 No README data            
    fetch@0.3.6 node_modules\fetch                             
    └── encoding@0.1.11 (iconv-lite@0.4.11)           

and it also exists in Github as Aurelia Navigation Skeleton app asks jspm get it from Github

``"fetch": "github:github/fetch@^0.9.0"`` 

##### Is this the same fetch? Why take it from Github and not npm? 

----

##Issue 3: 

This might not be any issue as ``github:systemjs/plugin-css@^0.1.11`` does not exists outside **jspm** domain so there is no problem where to take it from. This however needs to be explained in the README.md file 

----

###Complete package.json file for Aurelia Skeleton-Navigation application 0.17.0


    {
    "name": "aurelia-skeleton-navigation",
    "version": "0.17.0",
    "description": "A starter kit for building a standard navigation-style app with Aurelia.",
    "keywords": [
      "aurelia",
      "navigation",
      "skeleton"
    ],
    "homepage": "http://aurelia.io",
    "bugs": {
      "url": "https://github.com/aurelia/skeleton-navigation/issues"
    },
    "license": "MIT",
    "author": "Rob Eisenberg <rob@bluespire.com> (http://robeisenberg.com/)",
    "main": "dist/commonjs/index.js",
    "repository": {
      "type": "git",
      "url": "http://github.com/aurelia/skeleton-navigation"
    },
    "devDependencies": {
      "aurelia-cli": "^0.3.1",
      "aurelia-tools": "^0.1.3",
      "browser-sync": "^1.8.1",
      "conventional-changelog": "0.0.11",
      "del": "^1.1.0",
      "gulp": "^3.8.10",
      "gulp-babel": "^5.1.0",
      "gulp-bump": "^0.3.1",
      "gulp-changed": "^1.1.0",
      "gulp-jshint": "^1.9.0",
      "gulp-plumber": "^0.6.6",
      "gulp-protractor": "^0.0.12",
      "gulp-sourcemaps": "^1.3.0",
      "gulp-yuidoc": "^0.1.2",
      "jasmine-core": "^2.1.3",
      "jshint-stylish": "^1.0.0",
      "karma": "^0.12.28",
      "karma-babel-preprocessor": "^5.2.1",
      "karma-chrome-launcher": "^0.1.7",
      "karma-coverage": "^0.3.1",
      "karma-jasmine": "^0.3.5",
      "karma-jspm": "2.0.1-beta.2",
      "object.assign": "^1.0.3",
      "require-dir": "^0.1.0",
      "run-sequence": "^1.0.2",
      "vinyl-paths": "^1.0.0",
      "yargs": "^2.1.1"
    },
    "jspm": {
      "dependencies": {
        "aurelia-animator-css": "github:aurelia/animator-css@^0.15.0",
        "aurelia-binding": "github:aurelia/binding@^0.8.6",
        "aurelia-bootstrapper": "github:aurelia/bootstrapper@^0.16.0",
        "aurelia-dependency-injection": "github:aurelia/dependency-injection@^0.9.2",
        "aurelia-event-aggregator": "github:aurelia/event-aggregator@^0.7.0",
        "aurelia-fetch-client": "github:aurelia/fetch-client@^0.1.2",
        "aurelia-framework": "github:aurelia/framework@^0.15.0",
        "aurelia-history": "github:aurelia/history@^0.6.1",
        "aurelia-history-browser": "github:aurelia/history-browser@^0.7.0",
        "aurelia-loader": "github:aurelia/loader@^0.8.7",
        "aurelia-loader-default": "github:aurelia/loader-default@^0.9.5",
        "aurelia-logging": "github:aurelia/logging@^0.6.4",
        "aurelia-metadata": "github:aurelia/metadata@^0.7.3",
        "aurelia-path": "github:aurelia/path@^0.8.1",
        "aurelia-route-recognizer": "github:aurelia/route-recognizer@^0.6.2",
        "aurelia-router": "github:aurelia/router@^0.11.0",
        "aurelia-task-queue": "github:aurelia/task-queue@^0.6.2",
        "aurelia-templating": "github:aurelia/templating@^0.14.1",
        "aurelia-templating-binding": "github:aurelia/templating-binding@^0.14.0",
        "aurelia-templating-resources": "github:aurelia/templating-resources@^0.14.0",
        "aurelia-templating-router": "github:aurelia/templating-router@^0.15.0",
        "bootstrap": "github:twbs/bootstrap@^3.3.4",
        "clean-css": "npm:clean-css@^3.3.8",
        "core-js": "npm:core-js@^0.9.4",
        "css": "github:systemjs/plugin-css@^0.1.11",
        "fetch": "github:github/fetch@^0.9.0",
        "font-awesome": "npm:font-awesome@^4.3.0"
      },
      "devDependencies": {
        "babel": "npm:babel-core@^5.1.13",
        "babel-runtime": "npm:babel-runtime@^5.1.13",
        "core-js": "npm:core-js@^0.9.4"
      },
      "overrides": {
        "npm:core-js@0.9.18": {
          "main": "client/shim.min"
        }
      }
    }



* * *
* * *

 [1]: http://aurelia.io/docs.html
 [2]: http://stormpath.com
 [3]: http://blog.aurelia-guides.com/category/security/
 [4]: http://blog.aurelia-guides.com/2015/08/22/smallest-aurel…d-from-scratch
 [5]: https://www.npmjs.com/package/stormpath
 [6]: https://www.npmjs.com/
 [7]: http://jspm.io/
 [8]: https://github.com/systemjs/systemjs
 [9]: http://es6-features.org/
 [10]: http://javascriptplayground.com/blog/2014/11/js-modules-jspm-systemjs/
 [11]: http://blog.durandal.io/2015/05/06/getting-started-with-aurelia-and-typescript/

