```js
const video = {
  title: 'javascript',
  tags: [a,b,c],
  showTags() {
    this.tags.forEach(function(tag){
      console.log(this, tag); //callback function is a regular function (not an object method)
    })
  }
};

video.showTags();

//window a
//window b
//window c
```
