# Unserscore Collections

- __each__
- __map__
- reduce
- reduceRight
- find
- __filter__
- __where__
- findWhere
- reject
- every
- __some__
- contains
- invoke
- __pluck__
- __max__
- __min__
- __sortBy__
- __groupBy__
- indexBy
- countBy
- shuffle
- sample
- toArray
- __size__
- partition

## forEach: 迴圈執行所有子陣列

````
var List = new Backbone.Collection();

List.add([
  { title: 'Belgium', id: 1 },
  { title: 'China',   id: 2 },
  { title: 'Austria', id: 3 }
]);

console.log("-- forEach --");
List.forEach(function (model) {
  console.log(model.get('title'));
});
````

## sortBy: 依照指定鍵值排序

````
var List = new Backbone.Collection();

List.add([
  { title: 'Belgium', id: 1 },
  { title: 'China',   id: 2 },
  { title: 'Austria', id: 3 }
]);

var Sorted = List.sortBy(function (model) {
  return model.get("title").toLowerCase();
});

console.log("-- sortBy --");
Sorted.forEach(function (model) {
  console.log(model.get('title'));
});
````

## map: 將集合特定鍵值以另外建立於新的指標陣列中

````
var List = new Backbone.Collection();

List.add([
  { title: 'Belgium', id: 1 },
  { title: 'China',   id: 2 },
  { title: 'Austria', id: 3 }
]);

console.log("-- map --");    
console.log(List.map(function (model) {
  return model.get('title');
}));
````

## max/min: 取得集合特定鍵值最大與最小值

````
var List = new Backbone.Collection();

List.add([
  { title: 'Belgium', id: 1 },
  { title: 'China',   id: 2 },
  { title: 'Austria', id: 3 }
]);

console.log("-- max/min --");    
console.log("max: " + List.max(function (model) {
  return model.id;
}).id);

console.log("min: " + List.min(function (model) {
  return model.id;
}).id);
````

## pluck: 將集合特定鍵值以另外建立於新的指標陣列中

````
var List = new Backbone.Collection();

List.add([
  { title: 'Belgium', id: 1 },
  { title: 'China',   id: 2 },
  { title: 'Austria', id: 3 }
]);

var names = List.pluck('title');
console.log(JSON.stringify(names));
````

## any/some: 返回集合是否存在搜尋值

````
var List = new Backbone.Collection();

List.add([
  {name: 'Tom', score: 95, id: 1},
  {name: 'Rob', score: 75, id: 2},
  {name: 'Tim', score: 85, id: 3}
]);

console.log("-- any/some --");
console.log(List.some(function (model) {
  return model.get('name') == 'Rob';
}));
````

## size: 返回集合內model總數

````
var List = new Backbone.Collection();

List.add([
  {name: 'Tom', score: 95, id: 1},
  {name: 'Rob', score: 75, id: 2},
  {name: 'Tim', score: 85, id: 3}
]);

console.log("-- size --");
console.log(List.size());
````

## isEmpty: 檢查集合是否為空

````
var List = new Backbone.Collection();

console.log("-- isEmpty --");    
console.log(List.isEmpty());
````

## groupBy: 群組化 Collection

````
var List = new Backbone.Collection();

List.add([
  {name: 'Tom', score: 95, id: 1, passed: true},
  {name: 'Rob', score: 59, id: 2, passed: false},
  {name: 'Tim', score: 75, id: 3, passed: true}
]);

var newList = List.groupBy('passed');
var passedList = new Backbone.Collection(newList[true]);
var failedList = new Backbone.Collection(newList[false]);

console.log(JSON.stringify(passedList.pluck('name')));
console.log(JSON.stringify(failedList.pluck('name')));
````

## filter: 篩選特定欄位值

````
var myCollection = new Backbone.Collection();
myCollection.add([
  { title: 'Austria.', person: 2313,   continent: 'euro', id: 3 },
  { title: 'China.',   person: 135700, continent: 'asia', id: 2 },
  { title: 'Belgium.', person: 1120,   continent: 'euro', id: 1 }
]);

var filtered = myCollection.filter(function (model) {
  return model.get('continent') == 'euro';
});

filtered.forEach(function (model) {
  console.log(model.get('id') + ': ' + model.get('title'));
});
````

## where: 取得符合條件的 model 比較

````
var myCollection = new Backbone.Collection();
myCollection.add([
  { title: 'Austria.', person: 2313,   continent: 'euro', id: 3 },
  { title: 'China.',   person: 135700, continent: 'asia', id: 2 },
  { title: 'Belgium.', person: 1120,   continent: 'euro', id: 1 }
]);

var filtered = myCollection.where(function (model) {
  return model.get('continent') == 'euro';
});

console.log(filtered.length);
````