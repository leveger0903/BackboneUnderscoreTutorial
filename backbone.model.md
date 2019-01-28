# Backbone Model

- __extend__
- __initialize__
- __get__
- __set__
- escape
- has
- unset
- clear
- id
- idAttribute
- cid
- attribute
- changed
- defaults
- toJSON
- sync
- __fetch__
- __save__
- __destory__

## Model 基本宣告

````
var Model = Backbone.Model.extend({});
var myModel = new Model();
console.log(JSON.stringify(myModel));
````

## 建立一組隨即被調用的 Model

````
var Model = Backbone.Model.extend({
  
  // 宣告Model後即被調用
  initialize: function () {
    console.log('This model has been initialized');
  },

  // 預設參數
  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
console.log(JSON.stringify(myModel));
````

## 建立一組隨即被調用的 Model, 並覆寫預設的值

````
var Model = Backbone.Model.extend({
  
  initialize: function () {
    console.log('This model has been initialized');
  },

  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model({
  title: 'Kusanagi',
  company: 'ETtoday'
});
console.log(JSON.stringify(myModel));
````

## 取得 Model 內變數值

````
var Model = Backbone.Model.extend({
  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
console.log(myModel.get('title'));
````

## 變更 Model 內變數值

````
var Model = Backbone.Model.extend({
  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
myModel.set('title', 'Pohao');
console.log(myModel.get('title'));
````

## 在 Model 建立自定義方法

````
var Model = Backbone.Model.extend({
  defaults: {
    title: 'Kaoru',
    completed: false
  },
  setTitle: function (newTitle) {
    this.set({ title: newTitle });
  },
  getTitle: function () {
    return this.get('title');
  }
});

var myModel = new Model();
myModel.setTitle('Pohao');
console.log(myModel.getTitle());
````

## 移除 Model 內變數值

````
var Model = Backbone.Model.extend({
  defaults: {
    title: 'Kaoru',
    completed: false
  }
});

var myModel = new Model();
myModel.unset('title');
console.log(myModel.get('title'));
````

## Restful 資料交換

````
var GET = new Collection();
GET.fetch({
  data: $.param({ 
    token: '1234567890', 
    id: '4' 
  }),
  success: function (model, response, options) {
    myCollection.set(response, {remove: false});
  }, 
  error: function (model, response, options) {   
    console.log('error');
  }
});

# 建立新資料
myCollection.create(
  {
      title: 'go to Hell', 
      completed: true,
      id: 4 
  },
  {     
    success: function (model, response, options) { 
      console.log('success');
    }, 
    error: function (model, response, options) {   
      console.log('error');
    },
    wait: true
  }
);

# 更新既有資料
var PUT = myCollection.get(2);
PUT.save(
  { 
    title: 'go to Heaven', 
    completed: false,
    id: 1 
  }, 
  { 
    success: function (model, response, options) { 
      console.log('success');
    }, 
    error: function (model, response, options) {   
      console.log('error');
    },
    wait: true
  }
);

# 刪除資料
var DELETE = myCollection.get(1);
DELETE.destroy({
  data: $.param({ 
    token: '1234567890' 
  }),
  success: function (model, response, options) { 
    console.log('success');
  }, 
  error: function (model, response, options) {   
    console.log('error');
  },
  wait: true
});
````