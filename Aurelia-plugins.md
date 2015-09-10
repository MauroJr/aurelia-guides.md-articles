## Introduction 

This article is written in the form of a tutorial and the intent is to explain the benefits of Aurelia plugins [defined](http://aurelia.io/docs.html#plugins) as:

> A plugin is only a module with an exported ``configure function``. During startup Aurelia will load all plugin modules and call their ``configure`` functions, passing to them the FrameworkConfiguration instance so that they can configure the framework appropriately. Plugins can optionally return a ``Promise`` from their ``configure`` function in order to perform asynchronous configuration tasks. When writing a plugin, be sure to explicitly supply all metadata, including a View Strategy for Custom Elements.

>In order to do configuration on your plugin from within the app you can specify a function or object as the second argument to the configure function. Your plugin's configure function can then use that after your installation work is done. The consumer of your plugin might write code like this:
>```
>aurelia.use.plugin('plugin-name', config => { /* configuration work */ });


----------


## Example 1 - [Skeleton plugin](https://github.com/aurelia/skeleton-plugin)