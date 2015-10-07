# Introduction 

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
# What is a plugin really and how is it used? 

While the above described concept of an Aurelia plugin is not difficult to grasp (after all you can say that it is just an "DLL" - a dynamically linked library), there are details in both **creating** and **consuming** a plugin that need special attention and require detailed explanations. So, using the "mechanical" depiction of the relationship between the Aurelia application and a plugin (which literally is a container, lets start with the plugin construction first - to answer the first half of the question that serves as a title of this section. 

![](http://i.imgur.com/6kSaQ7m.png)

## Creating a plugin

Every plugin has to expose two endpoints (note that we called them "interface" and "export" just to get you to map several vocabularies together and be less confused by terminology). The Configuration endpoint allows plugin's adaptability to different (but still supported) use case scenarios.

In most general situation different developers **create** the plugin than developers that **use** the plugin as an external component to their application. This is not always the case, as application developer can create a plugin containing the code that is common for all applications this developer may have to develop. In either case the plugin creator has to have a very detailed knowledge of application developer's needs (so that the exported functionality fits the needs of as many developers as possible, while the opposite is not necessarily true; application developer only needs to understand the API that plugin exposes to the application that consumes that plugin. In other words, creating plugins is a lot more difficult than using them. This tutorial takes the position that the reader needs to understand both sides.
 
Plugin's Export Services endpoint is defined as a JavaScript code with the default name ``index.js`` which looks like (this is actual code for Aurelia-Bootstraper, referenced in the next section below - **Using (consuming a plugin)** 

```javascript
/*eslint no-unused-vars:0*/
import core from 'core-js';
import {Aurelia, LogManager} from 'aurelia-framework';

let logger = LogManager.getLogger('bootstrapper');
let readyQueue = [];
let isReady = false;

function onReady(callback) {
  return new Promise((resolve, reject) => {
    if (!isReady) {
      readyQueue.push(() => {
        try {
          resolve(callback());
        } catch (e) {
          reject(e);
        }
      });
    } else {
      resolve(callback());
    }
  });
}

export function bootstrap(configure: (aurelia:Aurelia) => void): Promise<void> {
  return onReady(() => {
    let loader = new window.AureliaLoader();
    let aurelia = new Aurelia(loader);

    return configure(aurelia);
  });
}
...

```

## Using (consuming a plugin)

In order to use the plugin, application needs to ensure that the plugin is "fetched" from some repository (npm registry, github, jspm registry are examples of such repository) and "stored" in the application's file structure. Such fetch takes place as a consequence:

- Reference a plugin in application's ``package.json`` file like

```
    ...
  },
"jspm": {
    "dependencies": {
      "aurelia-animator-css": "github:aurelia/animator-css@^0.16.0",
      "aurelia-binding": "github:aurelia/binding@^0.9.0",
      "bootstrapper": "github:aurelia/bootstrapper@^0.17.0",
	...
},
...
```
where we define that:

-  the origin for ``aurelia-bootstraper`` plugin to be [https://github.com/aurelia/bootstrapper](https://github.com/aurelia/bootstrapper)
- this plugin's "internal name to be "bootstrapper"

This "internal name" is subsequently used in the context of application's initialization code (typically the ``main.js`` that is the recommended application's entry point (place where the execution starts once the application is loaded in the browser):

```javascript
export function configure(aurelia) {
  aurelia.use
    .defaultBindingLanguage()
    .defaultResources()
    .history()
    .router()
    .eventAggregator()
    .boostrapper(),
...

  aurelia.start().then(a => a.setRoot('app', document.body));
}
```

----------

# End to end tutorial

A nice example of a plugin, which is also easy to understand and very well designed / implemented is the **[Aurelia-Application-Configuration](https://github.com/Vheissu/Aurelia-Configuration)** created by Dwayne Harrington from Brisbane, Australia. We will use this plugin to illustrate plugin creation and use with all gory details.

## Aurelia Application Configuration Plugin Creation

Let's call this plugin AAC plugin in the remainder of this text and start with the description of its purpose as defined by Dwayne Charrington, its author:

>  **AAC is a smart configuration plugin and singleton service layer for your Aurelia applications** 

Using a bit more formal language, AAC exposes (exports) a handful of methods that can be used at the time of your application's (application that uses AAC plugin) configuration phase. Let's list them here and you can see more details in the AAC plugin's **[README.md](https://github.com/Vheissu/Aurelia-Configuration#api)** file

- ``setCascadeMode(boolean = true)``
- ``setDirectory(name)``
- ``setConfig(fileName)``
- ``setEnvironment(environment)``
- ``setEnvironments(environments)``
- ``is(environment)``
- ``get(key, defaultValue = null)``
- ``set(key, val)``
- ``setAll(obj)``
- ``getAll()``

At this point we can explain the main sections of any plugin structure:

#### 1 Plugin Configuration Endpoint



#### 2 Plugin Services Endpoint
#### 3 Plugin Services Implementation

See **[Aurelia-Configuration/src/configure.js](https://github.com/Vheissu/Aurelia-Configuration/blob/master/src/configure.js)**



----------


## Aurelia Application Configuration Plugin Use

We will use the **[Aurelia Skeleton Navigation](https://github.com/aurelia/skeleton-navigation/releases/tag/0.18.1)** app (note that this link references the most current release 0.18.1). See also [Building Skeleton Navigation From Scratch](https://github.com/aurelia-guides/aurelia-guides.md-articles/blob/master/Building-Skeleton-Navigation-From-Scratch.md) for all details that will be used in this section.

----------

----------

----------


### Working notes (@jdanyov)

unfortunately an end-to-end tutorial does not exist to my knowledge. I have an idea for you if you want to push ahead and write this guide without a tutorial written by someone else: what you could do is take a look at the index.js files in each of the plugins I mentioned along with the instructions for usage in each of the libraries readme.md files. By pooling those examples and instructions you could probably create some pretty compelling original content for aurelia guides.

Aurelia is very very extensible so a plugin could do anything. Here's some examples:
- Plugins that provide general functionality like aurelia-dialog, aurelia-i18n, etc
- Some plugins provide resources like custom elements, custom attributes, value converters. In that case it's a matter of calling globalResources(...) in the plugin code.
- Other plugins register adapters to teach aurelia's binding system how to observe certain types of objects. Examples of this would be (aurelia-computed and aurelia-breeze).
- Then there are plugins that register custom implementations of standard aurelia components or monkey-patch standard aurelia components. Examples of this would be any of the animation plugins, also aurelia-async.
- A plugin could be any combination of the above. Does that help you?


