# Underscore Arrays

- first
- initial
- last
- rest
- compact
- flatten
- without
- union
- intersection
- difference
- uniq
- zip
- unzip
- object
- __indexOf__
- lastIndexOf
- sortedIndex
- findIndex
- findLastIndex
- range

## indexOf: 找出該物件於 Collection 的位置

````
var List = new Backbone.Collection();

List.comparator = function (a, b) {
  return a.get('score') < b.get('score') ? -1 : 1;
};

var student_a = new Backbone.Model({
  name: 'Tom', 
  score: 95, 
  id: 1
});

var student_b = new Backbone.Model({
  name: 'Rob', 
  score: 75, 
  id: 2
});

List.add([
  student_a, 
  student_b
]);

console.log("-- indexOf --");         
console.log((List.indexOf(student_b) === 0));
console.log((List.indexOf(student_a) === 1));
````