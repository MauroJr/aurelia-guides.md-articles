####Collection of snippets from https://gitter.im/Aurelia/Discuss

* * *

## A simple tab control (with Bootstrap for styling)
###Charles Pockert 

The following assumes you have included bootstrap in your application, though you can tweak the HTML to make it work with any CSS framework, or just style it yourself!

Comments have been added to explain the code

**tab-set.html**

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

**tab-set.js**

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


**tab.html**

    <template>
        <!-- Hide the tab's content if not visible -->
        <div class="${ contentVisible ? '' : 'hidden' }">
            <content>
            </content>
        </div>
    </template>

**tab.js**

    import {bindable} from 'aurelia-framework';

    export class Tab {
        @bindable heading = "Tab";
        contentVisible = false;

        bind(ctx) {
            this["$parent"] = ctx;
        }
    }

###An example of usage:

**some-view.html**

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


**some-view.js**

    export class SomeView {
      tabChanged(newTab) {
        console.log("Tab changed to: " + newTab);
      }
    }

----
----

## How to render different view structures in Aurelia?
### Matthew James Davis

I have a common html structure in my app.html in order to apply for all pages:

    <template>
    <require from="header"></require>
    <require from="side-bar"></require>
    <require from="theme-panel"></require>
    <require from="footer"></require>
    <!-- BEGIN HEADER -->
    <js-header></js-header>
    <!-- END HEADER -->
    
    <div class="clearfix"></div>
    
    <!-- BEGIN CONTAINER -->
    <div class="container">
        <div class="page-container">
            <!-- BEGIN SIDEBAR -->
            <js-side-bar></js-side-bar>
            <!-- END SIDEBAR -->
            <div class="page-content-wrapper">
                <div class="page-content">
                    <!-- BEGIN STYLE CUSTOMIZER(optional) -->
                    <js-theme-panel></js-theme-panel>
                    <!-- END STYLE CUSTOMIZER -->
                    <!-- BEGIN ACTUAL CONTENT -->
                    <div class="fade-in-up">
                        <router-view></router-view>
                    </div>
                    <!-- END ACTUAL CONTENT -->
                </div>
            </div>
        </div>
        <!-- BEGIN FOOTER -->
        <js-footer></js-footer>
        <!-- END FOOTER -->
    </div>
    <!-- END CONTAINER -->
    </template>
    

However, in my case, i have a login page with a totally different structure compared to others. In my app.js, i tried to use getViewStrategy() method to control which views i will render as following:

    activate(params, routeConfig, navigationInstruction){
        this.navigationInstruction = navigationInstruction;
        //console.log("params", params); // undefined
        //console.log("routeConfig", routeConfig); // undefined
        //console.log("navigationInstruction", navigationInstruction); // undefined
        //console.log("router", router); //undefined
    }
    getViewStrategy(){
        if(this.navigationInstruction == 'login'){
            return "app_login.html";
        } else {
            return "app.html";
        }
    }
    

in the code above, 'navigationInstruction' is undefined. Therefore, my solution cannot work well. Does anybody have another solution? Thanks so much!

##### Answer

Great question. In fact, when you have two totally sections of the same single page application, the right thing to do is create multiple root view models, or shells.

First, set your app up for custom initialization by adding `aurelia-app="main"` to your body tag, and creating a new initialization file correspondingly named `main.js`. It should look like this.

    export function configure(aurelia) {
      aurelia.use
        .standardConfiguration()
        .developmentLogging();
    
      // notice that we are setting root to 'login'
      aurelia.start().then(app => app.setRoot('login'));
    }
    

The `app.setRoot('login')` line tells Aurelia to load a file called `login.js` as the app root. This file should look similar to your current `app.js`. You can do anything you want in this file and it's corresponding view, and it will stay totally separate from your main app.

To navigate back to your main app, you'll need to call `app.setRoot('app')`, which means you'll need to inject the Aurelia object into your Login view model.

    import { inject, Aurelia } from 'aurelia-framework';
    
    @inject(Aurelia)
    export class Login {
      constructor(aurelia) {
        this.aurelia = aurelia;
      }
      goToApp() {
        this.aurelia.setRoot('app');
      }
    }
    

Answer provided by [Matthew James Davis][3] - see the full write-up here: [Aurelia Login Best Practices][4]

***
*** 
   
 [1]: https://gitter.im/Aurelia/Discuss
 [2]: https://chrome.google.com/webstore/detail/scribefire/elkkomimknapgodalnkjeddkjnjkfmfp
 [3]: http://stackoverflow.com/users/1981050/matthew-james-davis
 [4]: http://www.foursails.co/blog/aurelia-login-best-practices-pt-1/