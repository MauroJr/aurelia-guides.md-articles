## Introduction 

This article is written in the form of a tutorial and the intent is to explain the benefits of Aurelia plugins [defined](http://aurelia.io/docs.html#plugins) as:

> A plugin is only a module with an exported ``configure function``. During startup Aurelia will load all plugin modules and call their ``configure`` functions, passing to them the FrameworkConfiguration instance so that they can configure the framework appropriately. Plugins can optionally return a ``Promise`` from their ``configure`` function in order to perform asynchronous configuration tasks. When writing a plugin, be sure to explicitly supply all metadata, including a View Strategy for Custom Elements.

>In order to do configuration on your plugin from within the app you can specify a function or object as the second argument to the configure function. Your plugin's configure function can then use that after your installation work is done. The consumer of your plugin might write code like this:
>
>```javascript
>aurelia.use.plugin('plugin-name', config => { /* configuration work */ });
```

**Important note**: Aurelia framework itself is organized in the form of a single module that "uses" (``aurelia.use``) a collection of "plugins", many of them using other plugins. Here is the code for using  ``aurelia-computed`` in your application: (``aurelia-computed`` is defined as a plugin that improves the efficiency of Aurelia data-binding computed properties)  

```javascript
export function configure(aurelia) {
  aurelia.use
    .standardConfiguration()
    .developmentLogging()         // enable debug logging to see aurelia-computed's observability messages.
    .plugin('aurelia-computed');  // install the plugin

  aurelia.start().then(a => a.setRoot());
}
```


----------


## Example 1 - [Skeleton plugin](https://github.com/aurelia/skeleton-plugin)

The [Skeleton plugin](https://github.com/aurelia/skeleton-plugin) sample should be really called **Skeleton plugin tool**. It is a tremendous resource, capable of  creating 4 different dialects (amd, commonjs, es6 and system)  for the generated the Aurelia plugin object. The "skeleton" word in its name simply means that it is using the most simple set of source files that this plugin will "embedd" (listed below). 

**hello-world.html**

```html
<template>
  Hello, world!
</template>

```

**hello-world.js**
```javascript
export class HelloWorld {}

```


**index.js**
```javacript
export function configure(config){
  config.globalResources('./hello-world');
}
```

**Note 1** - observe that the ``hello-world.js`` file is E6 JavaScript, so the created ES6 plugin [code](https://github.com/aurelia/skeleton-plugin/blob/master/dist/es6/hello-world.js) is the same as the source code shown above. The generated amd [code](https://github.com/aurelia/skeleton-plugin/blob/master/dist/amd/hello-world.js) however is quite different:

```javascript
define(["exports"], function (exports) {
  "use strict";

  Object.defineProperty(exports, "__esModule", {
    value: true
  });

  function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError("Cannot call a class as a function"); } }

  var HelloWorld = function HelloWorld() {
    _classCallCheck(this, HelloWorld);
  };

  exports.HelloWorld = HelloWorld;
});
```


**Note 2** The "guts" of the plugin tool are in the gulp [build task](https://github.com/aurelia/skeleton-plugin/blob/master/build/tasks/build.js)

**Note 3** In order to illustrate the use of this ``hello-world`` plugin let's use the SAA sample - [Smallest Aurelia Application – created from scratch](http://blog.aurelia-guides.com/2015/08/22/smallest-aurelia-application-created-from-scratch/), slightly modified to allow the needed Aurelia configuration code, where we will "include" this plugin.

- change the file ``index.html`` to define the application's "entry point" to be ``main.js`` ( line ``<body aurelia-app="main">``)

```javascript
<!doctype html>
<html>
  <head>
    <title>Aurelia</title>
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

- Add the ``main.js`` file as shown below

```javascript
export function configure(aurelia) {
  aurelia.use
    .standardConfiguration()
    .developmentLogging()
    .hello-world();                  // <----- our plugin

  
  aurelia.start().then(a => a.setRoot());
}

```

