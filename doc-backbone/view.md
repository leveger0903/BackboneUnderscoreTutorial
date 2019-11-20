# Backbone View

- __extend__
- __initialize__
- __el__
- __$el__
- __setElement__
- attributes
- $(jQuery)
- __template__
- __render__
- remove
- __events__
- delegateEvents
- undelegateEvents

## 創建 View

````
var Model = Backbone.Model.extend();
var View = Backbone.View.extend({
  tagName: 'li',
  id: 'myList',
  className: 'myClass',
  template: _.template("List Template"),
  initialize: function() {
    this.render();
  },
  render: function () {
    this.$el.html(
      this.template( 
        this.model.toJSON() 
      )
    );

    return this;
  }
});

var myModel = new Model();
var myView = new View({ model: myModel });
console.log(myView.el);
````

## 創建 View, 當 el 有指定對象時

````
var View = Backbone.View.extend({
  el: $('#container')
});

var myView = new View();
console.log(myView.el);
````

## 創建View, 並賦予對象事件

````
var View = Backbone.View.extend({
  tagName: 'input',
  id: 'myList',
  className: 'myClass',
  template: _.template("List Template"),
  initialize: function () {
    this.render();
  },  
  render: function () {
    this.$el.html(this.template("List Template"));
    this.input = this.$('.edit');
    return this;
  },
  events: {
    'keydown': 'keyAction',
    'blur': 'keyBlur'
  },  
  keyAction: function (e) {
    if(e.which === 13)
      $('#container').append('<br>' + $('#myList').val());
  },
  keyBlur: function () {
    alert('結束新增事件');
  }
});

var myView = new View();
$('#container').append(myView.el);
````

## 將不同元件綁在相容的事件

````
$("#container").append('<input id="myButton" type="button" value="Hello"/>');

var View = Backbone.View.extend({
  initialize: function () {
    this.setElement($('#myButton'));
  },
  events: {
    'click': 'alertMsg'
  },
  alertMsg: function () {
    alert('說哈嘍')
  }
});

var myView = new View();
myView.setElement($('#myButton'));
````

## 在 jQuery 物件上產生指定物件

````
var View = Backbone.View.extend({
  el: $('#container'),
  initialize: function () {
    this.render()
  },
  render: function () {
    this.$el.append('<input type="text" placeholder="enter entities"/>');
    return this;
  }    
});

var myView = new View();
````

## View: jQuery.on()綁定事件

````
var View = Backbone.View.extend({
  el: '#myView',
  initialize: function () {
    this.$el.click(this.jqueryClicked);
  },
  jqueryClicked: function (e) {
    console.log('jQuery handler for' + this.outerHTML);
  },  
});

var view = new View();
````

## View:events 屬性綁定事件

````
var View = Backbone.View.extend({
  el: '#myView',
  events: {
    'click [type="checkbox"]': 'clicked'
  },
  initialize: function () {
    this.on('apiEvent', this.callback);
  },
  clicked: function (e) {
    console.log('events handler for ' + this.el.outerHTML);
    this.trigger('apiEvent', e.type);
  },
  callback: function (eType) {
    console.log('evnet type was ' + eType);
  }
});

var view = new View();
````