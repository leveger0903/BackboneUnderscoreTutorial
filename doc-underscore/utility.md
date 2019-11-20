# Underscore Utility

- noConflic
- identify
- constant
- noop
- times
- random
- mixin
- iteratee
- uniqueId
- escape
- unescape
- result
- now
- __template__

## template: 透過 ajax 取得模板並透過 jQuery 建構畫面

- underscore_template.html

````
<script id='bookTemplate' type='text/template'>
  <table style='border:1px solid #000;'>
    <thead>
      <tr>
        <th style='border:1px solid #000;'><%= titles.name     %></th>
        <th style='border:1px solid #000;'><%= titles.phone    %></th>
        <th style='border:1px solid #000;'><%= titles.sex      %></th>
        <th style='border:1px solid #000;'><%= titles.birthday %></th>
      </tr>
    </thead>
    </tbody>
      <% _.each(lists, function(item, key, list) { %>
      <tr>
        <td><%- item.name     %></td>
        <td><%- item.phone    %></td>
        <td><%- item.sex      %></td>
        <td><%- item.birthday %></td>
      </tr>
      <% }); %>
    </tbody>
  </table>
</script>
````

- underscore_script.js

````
var lists = [
  { 
    name: 'Orionis', 
    phone: '0412345678', 
    sex: 'male', 
    birthday: '1984-09-03' 
  },
  { 
    name: 'Morians', 
    phone: '0287654321', 
    sex: 'female', 
    birthday: '1987-08-12' 
  },
  { 
    name: 'Michael', 
    phone: '071234567', 
    sex: 'male',
    birthday: '1988-01-30' 
  },
];

var titles = {
  name:     '姓名',
  phone:    '電話',
  sex:      '性別',
  birthday: '生日'
};

var template;
$.get(
  'underscore3_template.html', 
  {}, 
  function (data) {
    $('#module').html(data);
    template = $('#bookTemplate').html();
    $('#container').html(_.template(
      template, 
      { lists: lists, titles: titles }
    ));
});
````

- main.html

````
<body>
  <div class="well">
      <h1>Under Score Template</h1>
      <div id="container"></div>
  </div>
  <div id='module'></div>
  <script src="underscore_script.js"></script>
</body>
````