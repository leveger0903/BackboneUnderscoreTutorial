# Backbone Collection Extend (Underscore)

- __add__ 
- __remove__
- __reset__
- set
- __get__
- at
- push
- pop
- unshift
- shift
- slice
- length
- comparator
- sort
- __pluck__
- where
- findWhere
- url
- parse
- clone
- __fetch__
- __create__

## Collection 新增 Model, 移除 Model

````
var Model = Backbone.Model.extend({
  default: {
    title: '',
    completed: false
  }
});

var Collection = Backbone.Collection.extend({
  model: Model
});

var myModelA = new Model({ title: 'Go to Taipei' }),
    myModelB = new Model({ title: 'Back to Taichung' }),
    myModelC = new Model({ title: 'Go to Kaohsung' });

var myCollection = new Collection([myModelA, myModelB]);
console.log("myCollection Size:" + myCollection.length);

myCollection.add([myModelC]);
console.log("myCollection Size:" + myCollection.length);

myCollection.remove([myModelA, myModelB]);
console.log("myCollection Size:" + myCollection.length);
````

## 檢索 Collection

````
var Model = Backbone.Model.extend({});
var Collection = Backbone.Collection.extend({});

var myModelA = new Model({ title: 'Allen', id: 2 }),
    myModelB = new Model({ tille: 'Ellie', id: 3 });

var myCollection = new Collection([myModelA, myModelB]);

var getData = myCollection.get(3);
console.log(getData === myModelA);
console.log(getData === myModelB);
````

## 利用 cid (backbone 的 uid) 檢索 Collection

````
var Model = Backbone.Model.extend({});
var Collection = Backbone.Collection.extend({});

var myModelA = new Model({ title: 'Allen', id: 2 }),
    myModelB = new Model({ tille: 'Ellie', id: 3 });

var myCollection = new Collection([myModelA, myModelB]);

var cid = myCollection.get(myModelB.cid);
console.log(cid === myModelA);
console.log(cid === myModelB);
````

## 使用 set 刷新集合 / reset 重置集合 (複合型範例)

````
var myCollection = new Backbone.Collection();

myCollection.add([
  { title: 'go to Jamaica',    completed: false, id: 1 },
  { title: 'go to China',      completed: false, id: 2 },
  { title: 'go to DisneyLand', completed: true,  id: 3 }
]);   

var collectionAction = {
  add: function (model) {
    console.log("Added " + model.get('title'));  
  },
  remove: function (model) {
    console.log("Removed " + model.get('title'));
  },
  reset: function (model) {
    console.log("Collection reset.");
  },
  change: function (model) {
    console.log("Completed " + model.get('title'));
  }
}

myCollection.on({
  'add'              : collectionAction.add,
  'remove'           : collectionAction.remove,
  'reset'            : collectionAction.reset,      
  'change:completed' : collectionAction.change
});

myCollection.set(
  [
    { title: 'go to Jamaica', completed: true, id: 1 },
    { title: 'go to China', completed: false, id: 2 },
    { title: 'go to DisneyLand', completed: false, id: 4 }
  ], 
  { remove: false }
); 
console.log('Collection size: ' + myCollection.length);

myCollection.reset([
  { title: 'go to Cuba', completed: true, id: 5 },
]); 
console.log('Collection size: ' + myCollection.length);  

myCollection.reset();
console.log('Collection size: ' + myCollection.length);
````

## RESTful 資料交換

- 參考 backbone.model 章節

## pluck 將集合特定鍵值另外建立於指標陣列之中

- 參考 underscore.collections 章節