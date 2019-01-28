# Backbone Sync

- __Backbone.sync__
- Backbone.ajax
- __Backbone.emulateHTTP__
- __Backbone.emulateJSON__

## 不使用 RESTful (PUT / DELETE)
Backbone.emulateHTTP = true;

## 不使用 JSON
Backbone.emulateJSON = true;

## Defer 與 Backbone.Sync 混用

* 參考: http://stackoverflow.com/questions/16476874/catching-backbone-sync-errors

````
Backbone.originalSync = Backbone.sync;
Backbone.sync = function (method, model, options) {
  var xhr, dfd;
  dfd = $.Deferred();

  if (options)
  	dfd.then(options.success, options.error);

  xhr = Backbone.originalSync(
    method, 
    model, 
    _.omit(options, 'success', 'error')
  );
  xhr.done(dfd.resolve);
  xhr.fail(function () {

    if (xhr.status === 200 && xhr.responseText === '') 
    {
      dfd.resolve.apply(xhr, arguments);
    } 
    else 
    {  
      if(
        xhr.status === 200 || 
        xhr.status === 302 || 
        xhr.status === 0
      ) {
      	console.log('login');
      }
      
      dfd.reject.apply(xhr, arguments);
    }
  });

  return dfd.promise();
};

var Model = Backbone.Model.extend({
  url: '/backbone/input.php'
});

var myModel = new Model();
var serverAction = myModel.save(null, {
  success: function () {
  	console.log('options success: ', arguments);
  },
  error: function () {
  	console.log('options error: ', arguments);
  }
});

serverAction.done(function () {
  console.log('success: ', arguments);
});

serverAction.fail(function () {
  console.log('fail: ', arguments);
});
````