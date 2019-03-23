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

# examples

https://jsbin.com/yapugucezi/edit?js,console
```js
let arr = [
  { product:'The Godfather', catalog:'movie',price:'150'},
  { product:'The Dark Knight', catalog:'movie',price:'100'},
  { product:'7 Rings', catalog:'music',price:'300'}
]

var arrFilter = arr.filter(function(item,index){
    if(item.catalog =="movie") {
      return true;
    }
})
console.log(arrFilter); //arr catalog:'music'

var arrSortPrice = arr.sort(function(a,b) {
    return b.price - a.price;
})
console.log(arrSortPrice); // arr 300 150 100  

let sum = 0;
arr.forEach(function(element) {
    sum+=parseInt(element.price);
});

console.log(sum); //sum price 550
```



### 陣列方法 `map()` 和 `forEach()` 有什麼區別？

這兩種方法都是對陣列中的元素進行迭代。  
`map()` 通過每個元素的回調函數將其映射到新的元素上，最終返回一個新的陣列。  
`forEach()` 雖然也為每一個元素準備了回調函數，但卻不返回新的陣列。  
`map()` 是**保持原有陣列不變的正確選擇**，他可以讓原始陣列的每一個值都映射到新的陣列上。    
`forEach()` 在每一次迭代的使用中都會產生副作用，因此 `map()` 是編程技術中常用的方法。  


如果你需要迭代一個陣列，使其本身發生變化且不需要返回一個新陣列時，可以使用 `forEach()`  
如果你只是對數字進行遍歷時，也可以使用 `forEach()`  

`map()` 運行的**較快**，且返回的新陣列可以讓你繼續使用 `map()、filter()、reduce()` 等方法，  

```js
const arr = [1, 2, 3, 4, 5];
const arr1 = arr.map(num => num * 2).filter(num => num > 5);
console.log(arr); // [1, 2, 3, 4, 5]
console.log(arr1); // [6, 8, 10]
```

ref: https://hacpai.com/article/1547790109416?r=Vanessa


