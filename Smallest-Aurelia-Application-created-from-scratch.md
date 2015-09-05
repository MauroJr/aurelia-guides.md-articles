####Summary
The purpose of this article is to create the smallest possible context to show perhaps the coolest feature of Aurelia, described as
> In Aurelia, user interface elements are composed of view and view-model pairs. The view is written with HTML and is rendered into the DOM. The view-model is written with JavaScript and provides data and behavior to the view. The templating engine and/or DI are responsible for creating these pairs and enforcing a predictable lifecycle for the process. Once instantiated, Aurelia's powerful databinding links the two pieces together allowing changes in your data to be reflected in the view and vice versa. This Separation of Concerns is great for developer/designer collaboration, maintainability, architectural flexibility, and even source control.

Once this context is created - the actual application consists of two files ``app.html``, referred to as the **view** and ``app.js`` called **view-model**. This is the smallest Aurelia app, mentioned in the title of this post

_This article is credited to **[Scott Allen](http://odetocode.com/about/scott-allen)** and **[Jeremy Danyow](http://www.danyow.net/)** - they both taught me how to use [jspm package manager](http://jspm.io/) to create the &quot;Hello World size&quot; Aurelia application. I want to include it in Aurelia-Guides repository so we can use it as a basic building block in the larger samples._

**Caveat**: This approach to to create Aurelia Application is not &quot;scholarly&quot; as it skips creation and use of many important parts of application&#39;s rigging - see **[starter kit for building a standard navigation-style app with Aurelia](https://github.com/aurelia/skeleton-navigation)** for all these details.

* * *

Assuming that all components of Aurelia Development Environment (see **[this](http://blog.aurelia-guides.com/2015/08/22/aurelia-development-environment-and-tools/)** for more details) are in place, create the folder for this project:

    mkdir minimal
    cd minimal

Now, let&#39;s start with **jspm** and to create the initial skeleton

    jspm init

This command results with following (note the warning - it&#39;s a smart thing to heed at least until **jspm** becomes production version so we do not need to worry about using the beta jspm.

    warn Running jspm globally, it is advisable to locally install jspm via npm install jspm --save
    -dev.                                                                                          
    Package.json file does not exist, create it? [yes]:                                            
    Would you like jspm to prefix the jspm package.json properties under jspm? [yes]:              
    Enter server baseURL (public folder path) [./]:                                                
    Enter jspm packages folder [.\jspm_packages]:                                                  
    Enter config file path [.\config.js]:                                                          
    Configuration file config.js doesn&#39;t exist, create it? [yes]:                                  
    Enter client baseURL (public folder URL) [/]:                                                  
    Do you wish to use an ES6 transpiler? [yes]:                                                   
    Which ES6 transpiler would you like to use, Babel or Traceur? [babel]:                         
    ok   Verified package.json at package.json                                                     
         Verified config file at config.js                                                         
         Looking up loader files...                                                                
           system.js                                                                               
           system-csp-production.js                                                                
           system.js.map                                                                           
           system.src.js                                                                           
           system-polyfills.js                                                                     
           system-polyfills.js.map                                                                 
           system-csp-production.js.map                                                            
           system-csp-production.src.js                                                            
           system-polyfills.src.js                                                                 

         Using loader versions:                                                                    
           systemjs@0.18.9                                                                         
         Looking up npm:babel-core                                                                 
         Looking up npm:babel-runtime                                                              
         Looking up npm:core-js                                                                    
         Updating registry cache...                                                                
         Looking up github:jspm/nodelibs-process                                                   
    ok   Installed babel as npm:babel-core@^5.8.21 (5.8.22)                                        
    ok   Installed github:jspm/nodelibs-process@^0.1.0 (0.1.1)                                     
         Looking up npm:process                                                                    
    ok   Installed npm:process@^0.10.0 (0.10.1)                                                    
    ok   Installed babel-runtime as npm:babel-runtime@^5.8.20 (5.8.20)                             
         Looking up github:jspm/nodelibs-fs                                                        
         Looking up github:systemjs/plugin-json                                                    
    ok   Installed github:jspm/nodelibs-fs@^0.1.0 (0.1.2)                                          
    ok   Installed github:systemjs/plugin-json@^0.1.0 (0.1.0)                                      
    ok   Installed core-js as npm:core-js@^1.0.0 (1.1.1)                                           
    ok   Loader files downloaded successfully                                                      

This single command (note that we accepted all of the defaults offered) results with the minimal project structure shown below:

<p align=center>
  <img src="http://i.imgur.com/jMFZG20.png"></img>
</p>

The highlighted sections of this image denote all EM6 related components that `jspm init` command created

Now, let us add Aurelia - meaning at least `aurelia-framework` and `aurelia-bootstrapper` packages need to be added to our application

    jspm install aurelia-framework
    jspm install aurelia-bootstrapper

Having the complete minimal infrastructure for Aurelia in place let's build our "Hello World" application itself.

Create the ``index.html`` file that will invoke the SystemJS module loader:

    <!doctype html>
    <html>
      <head>
        <title>Aurelia</title>
      </head>
      <body aurelia-app>
        <h1>Loading...</h1>

        <script src="jspm_packages/system.js"></script>
        <script src="config.js"></script>
        <script>
          System.import('aurelia-bootstrapper');
        </script>
      </body>
    </html>

By default, Aurelia Boostrap loader (``aurelia-bootstrapper``) expects the view model / view pair of files, named ``app``

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

This is really everything needed for the minimal Aurelia application - however in order to be compliant with "official Aurelia samples", we will also use two utilities

    npm install gulp --save-dev
    npm install browser-sync --save-dev

and provide the ``gulpfile.js``

    var gulp = require('gulp');
    var browserSync = require('browser-sync');

    // this task utilizes the browsersync plugin
    // to create a dev server instance
    // at http://localhost:9000
    gulp.task('serve', function(done) {
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

Now, start the web server using ``gulp``

    gulp serve

and point the browser:

    http://localhost:9000

you should see this:

<p align=center>
  <img src="http://i.imgur.com/gPifv0X.png"></img>
</p>

 The complete project's structure is this:

<p align=center>
  <img src="http://i.imgur.com/Gpgy5G8.png"></img>
</p>


**Note** due to its simplicity, this app will be used in several other articles where the accent is not on the Aurelia application but rather on how can Aurelia application connect to various services of interest.