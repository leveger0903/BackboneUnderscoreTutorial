# Backbone Events

- __on__
- __off__
- __trigger__
- __once__
- __listenTo__
- __stopListening__
- listenToOnce

## 建立 on 事件

````
var Model = Backbone.Model.extend({

  initialize: function () {
    console.log('This model has been initialized');
    this.on('change', function () {
      console.log(' - Values for this model have changed.');
    });
  },

  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
myModel.set({
  title: 'Pohao',
  completed: false
});
````

### 可用 on 事件清單：
- add
- remove
- update
- reset
- sort
- change
- change:[attribute]
- destory
- request
- sync
- error
- invalid
- route:[name]
- route
- all

## 事件監聽 (on) - add

````
var myCollection = new Backbone.Collection();

myCollection.on("add", function (data) {
  console.log("I should " + data.get("title") + ". Have I done it before? " + (data.get("completed") ? "Yeah!" : "No."));
});

myCollection.add([
  { title: 'go to Jamaica',    completed: false },
  { title: 'go to China',      completed: false },
  { title: 'go to DisneyLand', completed: true  },
]);
````

## 事件監聽 (on) - change:title

````
var myCollection = new Backbone.Collection();

myCollection.on("change:title", function (data) {
  console.log("Changed my mind! I should " + data.get("title"));
});

myCollection.add([
  { title: 'go to Jamaica',    completed: false, id: 1 },
  { title: 'go to China',      completed: false, id: 2 },
  { title: 'go to DisneyLand', completed: true,  id: 3 }
]);    

var myModel = myCollection.get(3);
myModel.set('title' , 'go to Hong Kong');
````

## 多組事件監聽 (on)

````
var myCollection = new Backbone.Collection();

myCollection.on({
  'change:title' : titleChanged,
  'change:completed' : stateChanged
});

function titleChanged(model) {
  console.log('The title was changed: ' + model.get('title'));
}

function stateChanged(model) {
  console.log('The state was changed: ' + model.get('completed'));
}

myCollection.add([
  { title: 'go to Jamaica',    completed: false, id: 1 },
  { title: 'go to China',      completed: false, id: 2 },
  { title: 'go to DisneyLand', completed: true,  id: 3 }
]);

var myModel = myCollection.get(3);
myModel.set('title' , 'go to Hong Kong');
myModel.set('completed' , false);
````

## 一次性事件驅動 (once)

````
var myObject = { itemA: 0, itemB: 0 };
_.extend(myObject, Backbone.Events);

myObject.once('event', function () {
  myObject.itemA += 1;
  myObject.trigger('event');
});

myObject.once('event', function () {
  myObject.itemB += 1;
});

myObject.trigger('event');

console.log(myObject.itemA === 1);
console.log(myObject.itemB === 1);
````

## 事件驅動 (trigger), 事件綁定 (on), 解除事件綁定 (off)

````
var action = {};
_.extend(action, Backbone.Events);

function subscribeAction (account) {
  console.log('subscriber: ' + account);
}

#事件綁定.事件驅動
action.on('subscribe', subscribeAction);
action.trigger('subscribe', 'orionis.kahza');

#解除事件綁定.事件驅動
action.off('subscribe', subscribeAction);
action.trigger('subscribe', 'orionis.kahza');
````

## 任意事件驅動

````
var action = {};
_.extend(action, Backbone.Events);

action.on('all', function (account, name) {
  console.log('subscriber: ' + name);
});

action.trigger('subscribe', 'orionis.kahza');
action.trigger('order', 'nirovsk.sofer');
````

## 子事件驅動

````
var action = {};
_.extend(action, Backbone.Events);

action.on('subscribe:byAccount', function (name) {
  console.log('subscriber: ' + name);
});

action.on('subscribe:byEmail', function (mail) {
  console.log('subscriber: ' + mail);
});

action.trigger('subscribe:byAccount', 'orionis.kahza');
action.trigger('subscribe:byEmail', 'kaoru.tseng@ettoday.net');
````

## 帶入多值與同時驅動多事件

````
var action = {};
_.extend(action, Backbone.Events);

function subscribeAction (account, name, email) {
  console.log('subscriber: ' + account + ' | name:' + name + ' | email:' + email);
}

action.on('subscribe', subscribeAction);
action.on('order', subscribeAction);

action.trigger('subscribe', 'orionis.kahza', 'orionis.kahza', 'kaoru.tseng@ettoday.net');
action.trigger('order', 'arden.kahza', 'arden.kahza', 'arden.kahza@chyp.com.tw');
````

## 監聽另一對象特定事件, 或是解除另一事件

````
var selfEvent   = _.extend({}, Backbone.Events);
var listenEvent = _.extend({}, Backbone.Events);

selfEvent.listenTo(listenEvent, 'anything', function (event) {
  console.log('anything happened');
});

listenEvent.trigger('anything');

selfEvent.stopListening();
listenEvent.trigger('anything');
````

## View 銷毀, 即將所有監聽事件一併解除

````
var view = new Backbone.View();
var listenEvent = _.extend({}, Backbone.Events);

view.listenTo(listenEvent, 'anything', function (event) { 
  console.log('anything happened'); 
});

listenEvent.trigger('anything');

view.remove();
listenEvent.trigger('anything');
````

## 一次性事件監聽

````
var selfEvent   = _.extend({}, Backbone.Events);
var listenEvent = _.extend({}, Backbone.Events);

selfEvent.listenToOnce(listenEvent, 'anything', function (event) {
  console.log('anything happened');
});

listenEvent.trigger('anything');
listenEvent.trigger('anything');
````