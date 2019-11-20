# Backbone Collection

- __extend__
- model
- modelId
- initialize
- models
- toJSON
- sync

## Collection 的初始

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
````

## 相同元素結合

````
var myCollection = new Backbone.Collection();

myCollection.add([
  {id: 1, name: 'Taipei',   pop: '200M'},
  {id: 2, name: 'Taichung', pop: '160M'},
  {id: 3, name: 'Kaohuung', pop: '140M'}
 ]);
console.log(JSON.sringify(myCollection));

#不會被複寫
myCollection.add([
    {id: 1, name: 'Tainan', pop: '100M'}
]);
console.log(JSON.sringify(myCollection));

#會被複寫
myCollection.add(
  [
    {id: 2, name: 'Tainan', pop: '100M'}
  ], 
  { merge: true }
);
console.log(JSON.sringify(myCollection));
````

## 查看 Collection 被更動前的內容

````
var myCollection = new Backbone.Collection();

myCollection.add([
  { title: 'go to Jamaica',    completed: false, id: 1 },
  { title: 'go to China',      completed: false, id: 2 },
  { title: 'go to DisneyLand', completed: true,  id: 3 }
]); 

myCollection.on('reset', function (Model, Options) {
  console.log(Options.previousModels[1].get('title'));
});

myCollection.reset([
  { title: 'go to Cuba', completed: true, id: 5 },
]);
````

