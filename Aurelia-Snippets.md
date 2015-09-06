Collection of snippets from https://gitter.im/Aurelia/Discuss

* * *

# A simple tab control (with Bootstrap for styling)

The following assumes you have included bootstrap in your application, though you can tweak the HTML to make it work with any CSS framework, or just style it yourself!

Comments have been added to explain the code

**tab-set.html**
```HTML
<template>
    <!-- Create a ul element for the clickable tabs -->
    <ul class="nav nav-tabs">
        <!--  Repeat over each `tab` in the `tabs` collection - note that the class is also 
        programatically chosen based on if the current tab === the selected tab --> 
        <li role="presentation" click.delegate="$parent.selectTab(tab)" repeat.for="tab of tabs" class="${ $parent.selectedTab === tab ? 'active' : '' }"><a href="#">${ tab.heading }</a></li>
    </ul>
    
    <!--Use a content selector to pull in any children of the custom element (the tabs themselves) -->
    <div>
        <content></content>
    </div>
</template>
```

**tab-set.ts**
```Javascript
import {sync, bindable} from 'aurelia-framework';

// The sync decorator uses a DOM mutation observer to look for changes
// in the DOM. When changes occur, it runs the specified CSS selector 
// and picks up the matched elements. An array property is added to your
// viewmodel class with the specified name. The array will contain the
// elements themselves or if they are backed by viewmodels will contain
// the viewmodel instances 
@sync({ name: "tabs", selector: "tab" })
export class TabSet {
    // This will be a collection of tabs that are children of the custom element tag
    tabs = [];
    
    @bindable selectedTab  = null;
    @bindable selectedIndex = 0;

    // This is a bindable callback that will fire when the selected tab changes
    @bindable tabChanged;

    // This allows the parent viewmodel to be referenced as `$parent`
    bind(ctx) {
        this["$parent"] = ctx;
    }

    selectedTabChanged() {
        this.onTabChanged();
    }

    tabsChanged() {
        if (this.tabs.length > 0) {
            if (this.selectedIndex >= this.tabs.length)
                this.selectedTab = this.tabs[0];
            else
                this.selectedTab = this.tabs[this.selectedIndex];
        }
        else
            this.selectedTab = null;   

        this.updateVisibility();
    }

    onTabChanged() {
        // Raise the event if a tab changes
        if (this.tabChanged)
            this.tabChanged(this.selectedTab);
    }

    selectTab(tab: any) {
        this.selectedTab = tab;

        // Find tab index
        var i = 0;
        this.tabs.forEach(t => { if (t === this.selectedTab) this.selectedIndex = i; i++ })

        this.updateVisibility();
    }

    updateVisibility() {
        this.tabs.forEach(tab => {
            tab.contentVisible = tab === this.selectedTab;
        });
    }
}
```

**tab.html**
```HTML
<template>
    <!-- Hide the tab's content if not visible -->
    <div class="${ contentVisible ? '' : 'hidden' }">
        <content>
        </content>
    </div>
</template>
```

**tab.js**
```Javascript
import {bindable} from 'aurelia-framework';

export class Tab {
    @bindable heading = "Tab";
    contentVisible = false;

    bind(ctx) {
        this["$parent"] = ctx;
    }
}
```

An example of usage:

**some-view.html**
```HTML
<template>
  <require from="tab-set"></require>
  <require from="tab"></require>
  
  <tab-set tab-changed.call="tabChanged($event)">
    <tab heading="Tab 1">
      <p>Hello</p>
    </tab>
    <tab heading="Tab 2">
      <p>World</p>
    </tab>
</template>
```

**some-view.js**
```Javascript
export class SomeView {
  tabChanged(newTab) {
    console.log("Tab changed to: " + newTab);
  }
}
```
