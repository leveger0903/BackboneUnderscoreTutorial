# Underscore Objects

- __keys__
- allKeys
- __values__
- mapObject
- __pairs__
- invert
- create
- functions
- findKey
- extend
- extendOwn
- __pick__
- __omit__
- defaults
- clone
- tap
- has
- matcher
- property
- propertyOf
- isEqual
- isMatch
- __isEmpty__
- isElement
- isArray
- isObject
- isArguments
- isFunction
- isString
- isNumber
- isFinity
- isBoolean
- isDate
- isRegExp
- isError
- isNaN
- isNull
- isUndefined

## pick: 取得該物件部分指定值

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ title: 'Austria', miles: 50, tier: 3 });

console.log('-- pick --');
console.log(myModel.pick(['title', 'miles']));
````

## omit: 排除該物件部分指定值

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ title: 'Austria', miles: 50, tier: 3 });

console.log('-- omit --');
console.log(myModel.omit(['miles', 'tier']));
````

## key: 取得所有物件鍵值

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ title: 'Austria', miles: 50, tier: 3 });

console.log("-- keys --");    
console.log(myModel.keys());
````

## values: 取得所有物件變數值

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ title: 'Austria', miles: 50, tier: 3 });

console.log("-- values --");    
console.log(myModel.values());
````

## pairs: 將物件鍵值 / 變數值分別轉為成對的array

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ title: 'Austria', miles: 50, tier: 3 });

# [
#   ["title", "Austria"],
#   ["miles", 50],
#   ["tier", 3]
# ]
console.log(JSON.stringify(myModel.pairs()));
````

## invert: 將物件鍵值與變數值顛倒

````
var Model = Backbone.Model.extend({});
var myModel = new Model({ 
  city: 'SanFrancisco', 
  state: 'California', 
  country: 'UnitedStates' 
});

console.log("-- invert --");    
console.log(myModel.invert());
````