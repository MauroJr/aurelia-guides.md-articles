Start with the finished application built in the tutorial **[Smallest-Aurelia-Application-created-from-scratch](http://blog.aurelia-guides.com/2015/08/22/smallest-aurelia-application-created-from-scratch/)**

Use the information presented in **[Aurelia get started](http://aurelia.io/get-started.html)**, section **Adding Navigation**. So, we have to change the existing app.js first

####app.js

    import 'bootstrap';
	import 'bootstrap/css/bootstrap.css!';

	export class App {
	  configureRouter(config, router){
	    config.title = 'Aurelia';
	    config.map([
	      { route: ['','welcome'], name: 'welcome', moduleId: 'welcome', nav: true, title:'Welcome' }
	    ]);

	    this.router = router;
	  }
	}

**Note** the change in the application title - just to differentiate it from the sample presented in the **[Aurelia get started](http://aurelia.io/get-started.html)** tutorial.

and then the **view** next

####app.html

    <template>
	  <nav class="navbar navbar-default navbar-fixed-top" role="navigation">
	    <div class="navbar-header">
	      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
	        <span class="sr-only">Toggle Navigation</span>
	        <span class="icon-bar"></span>
	        <span class="icon-bar"></span>
	        <span class="icon-bar"></span>
	      </button>
	      <a class="navbar-brand" href="#">
	        <i class="fa fa-home"></i>
	        <span>${router.title}</span>
	      </a>
	    </div>

	    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
	      <ul class="nav navbar-nav">
	        <li repeat.for="row of router.navigation" class="${row.isActive ? 'active' : ''}">
	          <a href.bind="row.href">${row.title}</a>
	        </li>
	      </ul>

	      <ul class="nav navbar-nav navbar-right">
	        <li class="loader" if.bind="router.isNavigating">
	          <i class="fa fa-spinner fa-spin fa-2x"></i>
	        </li>
	      </ul>
	    </div>
	  </nav>

	  <div class="page-host">
	    <router-view></router-view>
	  </div>
	</template>

Since we are using ``bootstrap`` package, we need to tell ``jspm`` to fetch it:

``jspm install github:twbs/bootstrap``

