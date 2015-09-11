## Introduction 

This article is written in the form of a tutorial and the intent is to explain the benefits of Aurelia plugins [defined](http://aurelia.io/docs.html#plugins) as:

> A plugin is only a module with an exported ``configure function``. During startup Aurelia will load all plugin modules and call their ``configure`` functions, passing to them the FrameworkConfiguration instance so that they can configure the framework appropriately. Plugins can optionally return a ``Promise`` from their ``configure`` function in order to perform asynchronous configuration tasks. When writing a plugin, be sure to explicitly supply all metadata, including a View Strategy for Custom Elements.

>In order to do configuration on your plugin from within the app you can specify a function or object as the second argument to the configure function. Your plugin's configure function can then use that after your installation work is done. The consumer of your plugin might write code like this:
>
>```javascript
>aurelia.use.plugin('plugin-name', config => { /* configuration work */ });
```

**Important note**: Aurelia framework itself is organized in the form of a single module that "uses" a collection of "plugins", many of them using plugins. Here is the code for using  ``aurelia-computed`` in your application: (``aurelia-computed`` is defined as a plugin that improves the efficiency of Aurelia data-binding computed properties)  

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