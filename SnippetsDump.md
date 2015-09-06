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


