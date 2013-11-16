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

### Fast Start

```html
<Template name="test">
  {{#each people}}
    {{name}}:{{age}}
  {{/each}}
  {{{pager}}}
</Template>
```


```js
var page = new Pagination("myfirstPagination");

Template.test.people = function(){
  return People.find({},page.skip());
}

Template.test.pager = function(){  //Note : pager was  surrounded by three '{}'. example {{{pager}}} 
  return page.create(People.find().count());
}

Template.test.destroyed = function(){
  page.destroy();
}
```

It's important to note that arguments of Pagination Construction is id  of pagination dom;and there are two paramters

### Pagination Construction

```js
/*
*
*identifier  Tyep:String
      the pagination' identifier .Be sure it's only.Relying on it distinguish different pagination if there are two or more {{{pager}}} on the same Template. 
*options  Type:Object  [optional parameter]
*    perPage :Set the number of results you want to display per page.  default 1
*    currentPage:Set the current page . default 10
*    e.g {currentPage: 1,perPage:10}  
*/
Pagination = function(identifier,options){}
```
### go
Set the number of results you want to display per page by not auto. 
you can do it use Pagination's instance.
```js
  page.go(2);
```
or call Pagination.go by Pagination's identifier

```js
  Pagination.go("myfirstPagination",2);
```

*Pagination.go(identifier,page)
  *identifier : pagination's
  *page: the page what you want to show

### destroy
  *you had better destroy Pagination when your Template destroy. because the some date about pagination keep in memory.
  *for example:
```js
Template.test.destroyed = function(){
  page.destroy();
}
```
or call Pagination.destroy by Pagination's identifier

```js
  Pagination.destroy("myfirstPagination");
```

### skip
you just only use it on Collection; the skip tell the Collection how to show the data by  paging.

```js
  Template.test.people = function(){
    return People.find({},page.skip());
  }
```

## create

create the Pagination on html

you only do it like this:

```html
<Template name="test">
  {{{pager}}}
</Template>
```

```js
Template.test.pager = function(){
  return page.create(People.find().count());
}
```


### The result 
  
  result work with [Bootstrap pagination](http://twitter.github.com/bootstrap/components.html#pagination) 

    ```html
    <div class="pagination">
      <ul>
        <li><a href="#">«</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#" class="active">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">»</a></li>
      </ul>
    </div>