## map 

對元素重新組裝，生成新陣列
[Array.prototype.map()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map)  

https://jsbin.com/xevunu/edit?js,console
```js
var arr = [1, 2, 3];
var arr2 = arr.map(function(item,index){
    return '<b>'+item+'</b>';

})
console.log(arr2);
// expected output: ["<b>1</b>", "<b>2</b>", "<b>3</b>"]
```

```js
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```
