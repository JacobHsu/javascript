title: Array methods
---

# Array

## forEach 

遍歷所有元素
[Array.prototype.forEach()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)  

https://jsbin.com/xoninaz/edit?js,console

```js
var arr = [1, 2, 3];

arr.forEach(function(item,index) {
  console.log(item,index);
});

// expected output: 1 0
// expected output: 2 1 
// expected output: 3 2 
```

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

##  filter 

過濾符合條件的元素，生成新陣列
[Array.prototype.filter()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) 


https://jsbin.com/xoninaz/1/edit?js,console
```js
var arr = [1, 2, 3];
var arr2 = arr.filter(function(item,index){
    if(item>2) {
        return true;
    }
})
console.log(arr2); 
// expected output: [3]
```

## find

回傳第一個滿足所提供之測試函式的元素值。否則回傳 undefined  
[Array.prototype.find()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/find)  


https://jsbin.com/qapevom/edit?js,console
```js
var arr = [1, 2, 3];
var found = arr.find(function(item,index){
    return item>1;
})
console.log(found);
// expected output: 2
```

## sort 

對一個陣列的所有元素進行排序，並回傳此陣列  
[Array.prototype.sort()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)  

https://jsbin.com/gaceyen/edit?js,console

```js
var arr = [1, 4, 2, 3, 5];
var arr2 = arr.sort(function(a,b){
    return a - b; //從小到大排序
    //return b - a; //從大到小排序
})
console.log(arr2); 
// expected output: [1, 2, 3, 4, 5]
```

## every 

測試陣列 判斷所有元素是否都符合條件
[Array.prototype.every()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

https://jsbin.com/nefobuh/edit?js,console

```js
var arr = [1, 2, 3];
var result = arr.every(function(item,index){
  if(item<4) {
    return true;
  }
})
console.log(result);
// expected output: true
```


## some 

測試陣列 判斷是否至少一個元素符合條件
[Array.prototype.some()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

https://jsbin.com/yeleboz/edit?js,console
```js
var arr = [1, 2, 3];
var result = arr.some(function(item,index){
  if(item<2) {
    return true;
  }
})
console.log(result);
// expected output: true
```




