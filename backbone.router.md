# Backbone Router

- __extend__
- __routes__
- __initialize__
- route
- __navigate__
- execute

## 使用 hash(#) 路由

````
var Router = Backbone.Router.extend({
  routes: {
    #http://localhost/#about
    'about' : 'aboutPage',
    #http://localhost/#search/job
    'search/:query' : 'searchPage',
    #http://localhost/#serach/job/1
    'search/:query/:page' : 'searchPages',
    #http://localhost/#other
    '*other' : 'defaultRoute'
  },
  aboutPage: function () {
    console.log('[about page]');
  },
  searchPage: function (query, page) {
    var page_number = page || 1;
    console.log('[search page]');
    console.log('query: ' + query);
    console.log('page number: ' + page_number);
  },
  defaultRoute: function (other) {
    console.log('[default]');
    console.log('keyword: ' + other);
  }
});

var myRouter = new Router();
Backbone.history.start();
````

## 變更路由 (navigate)

````
var Router = Backbone.Router.extend({
  routes: {
    'page/:id': 'viewPage',
    'page/:id/edit': 'editPage'
  },
  viewPage: function (id) {
    console.log('View page requested.');
    this.navigate('todo/' + id + '/edit', {trigger: 'true'});
  },
  editPage: function (id) {
    console.log('Edit page opened.');
  }
});

var myRouter = new Router();
Backbone.history.start();
````

## 抓取路由資訊

````
var Router = Backbone.Router.extend({
  routes: {}
});

var myRouter = new Router();
Backbone.history.start();

myRouter.on('route', function (name, args) {
  console.log(name);
  console.log(args);
});
````