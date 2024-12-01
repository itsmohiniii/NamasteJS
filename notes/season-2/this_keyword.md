```js
const video = {
  title: 'javascript',
  tags: ['a', 'b', 'c'],
  showTags() {
    //here, this refers to video object
    this.tags.forEach(function(tag){
      console.log(this, tag); //callback function is a regular function (not an object method)
    })
  }
};

video.showTags();

//window 'a'
//window 'b'
//window 'c'
```


```js
const video = {
  title: 'javascript',
  tags: ['a', 'b', 'c'],
  showTags() {
    //here, this refers to video object
    this.tags.forEach(function(tag){
      console.log(this.title, tag); //callback function is a regular function (not an object method)
    }, this)
  }
};

video.showTags();

//'javascript' 'a'
//'javascript' 'b'
//'javascript' 'c'
```
