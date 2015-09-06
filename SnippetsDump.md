## Please add your snippets / tags / comments here. 
This file will be regularly processed by Aurelia-Guides folks and place the info on the right place.


## Styling Template Components 

Given a template you can apply styling to it in a variety of manners. If you have
difficulty locating the file, you may need to be explicit and use relative paths: ```"./some-file"```

### Importing

At the top of your view-model add: ```import 'nav-bar.css!'```. Note the exclamation mark. 
This approach requires you install (via terminal) the system.js add-on for css:

```
jspm install css
```

### Style Attribute

!!! actually this doesn't work for me, but I think should. !!!


```
import {style} from 'aurelia-framework'

@style("nav-bar.css")
export class NavBar {
```

### View Requirement

Rather that import the styling in the view-model you can load it via the view itself with the require directive:

```
<template> 
  <require from="./nav-bar.css" />
  ...
  </template>
```

#My bits (Charles Pockert)

# Importing styles in view-models/views

###As an import in the view (using plugin-css plugin for SystemJS):

```Javascript
// Absolute paths are from the baseURI which is the "*" in your config.js
import "absolute/path/to/style.css!";
// Relative imports are relative to the consuming module:
import "../../relative/path/to/style.css!";
// e.g. import from current folder:
import "./style.css!";
```

* Note, the ! above is to let SystemJS know that you want to load the file using a plugin. The plugin will automatically be selected using the file extension. You can force a plugin by providing the plugin name after the !. See the very last section here: https://github.com/systemjs/systemjs/blob/master/docs/overview.md#plugins

**Warning:** 
At the time of writing in SystemJS, since module loading is async there is no way to guarantee the order of injection for imported CSS files. 

###In a view:

Loading styles in views has changed; previously Aurelia was using HTML Imports to load styles like so:

```HTML
<link rel="import" href="path/to/style.css"></link>
<template>
</template>
```

This will no longer work as of framework version 0.15.0

The correct way is to use `<require>` as per module imports:

```HTML
<template>
  <require from="path/to/style.css"></require>
</template>
```

**Note, the `<require>` tag MUST be inside the template** - it will cause an error in the framework if placed outside the template as Aurelia expects the first element in the DOM to be the `template` tag.
