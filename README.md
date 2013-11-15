Meteor Pagination
==============================================
The project github:https://github.com/huyinghuan/meteor-pagination-mini.git
The project come from https://github.com/airlok/meteor-pagination cloning.
Thanks for @airlok 

#### this package is  depends jquery and bootstrap

This enables simple pagination in your Meteor app. There are two key parts:

   Limiting cursor results to only what should be displayed on the current page.
   Displaying page links at the bottom, the styles just for bootstrap.

## Basics

Displaying only the current page's cursor results is easy. This will enable you to insert just those results into each page, and it automatically changes when the page changes. 

### Example

```html
<Template name="test">
  {{#each people}}
    {{name}}:{{age}}
  {{/each}}
  <div class="pagination" id="testPagination">
  </div>
</Template>
```


```js
var page = new Pagination("testPagination");

Template.test.people = function(){
  return People.find({},page.skip());
}

Template.test.rendered = function(){
  page.create(People.find().count());
}

Template.test.destroyed = function(){
  page.destroy();
}
```

It's important to note that arguments of Pagination Construction is id  of pagination dom;and there are two paramters


```js
/*
*
*seletor  Tyep:String  
  id of pagination dom
*options  Type:Object  [optional parameter]
*    perPage :Set the number of results you want to display per page.  default 1
*    currentPage:Set the current page . default 10
* e.g {currentPage: 1,perPage:10}  
*/
Pagination = function(selector,options){}
```




Set the number of results you want to display per page by not auto. 

  page.go(2);


### The result 
  
    result work with [Bootstrap pagination](http://twitter.github.com/bootstrap/components.html#pagination) 

    ```html
    <div class="pagination" id="testPagination">
      <ul>
        <li><a href="#">«</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#" class="active">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">»</a></li>
      </ul>
    </div>