# Backbone Model Extend (Underscore)

- validate
- validationError
- isValid
- __url__
- __urlRoot__
- parse
- clone
- isNew
- __hasChanged__
- changedAttributes
- previous
- previousAttributes

## 偵測 Model 內參數被改變

````
var Model = Backbone.Model.extend({
  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
console.log('title has changed:' + myModel.hasChanged('title'));
myModel.set('title', 'Pohao');
console.log('title has changed:' + myModel.hasChanged('title'));
````

## 條件驗證, 失敗時返回訊息

````
var Model = Backbone.Model.extend({
  defaults: {
    name: 'Kaoru',
  },
  validate: function (attrs, options) {
    if (!attrs.name) {
      return "please set name";
    }
  }
});

var myModel = new Model();
myModel.on('invalid', function (model, error) {
  console.log(error);
});
myModel.unset('name', {validate: true});
````

## 驗證條件, 在起始時

````
var Model = Backbone.Model.extend({
  default: {
    completed: false
  },
  validate: function (attrs, options) {
    if(attrs.title == undefined)
      return "please set name";
  },
  initialize: function () {
    console.log('This model has been initialized');
    this.on('invalid', function (model, error) {
      console.log(error);
    });
  }
});

var myModel = new Model();
myModel.set('completed', true, {validate: true});
myModel.set('title', 'Orionis', {validate: true});
````

## 變更 Restful 的 URL (urlRoot.url - POST / PUT)

````
var Model = Backbone.Model.extend({
  defaults: {
    title: '',
    completed: false
  },
  urlRoot: '/Backbone/',
  url: function (model) {
    // 產生路徑為http://localhost/Backbone/input.php?id=1
    return 'input.php?id=' + this.get('id');
  } 
});
````