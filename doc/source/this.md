title: This
---

## 物件的方法調用 (As an object method)

物件下呼叫會影響 `this` 的指向

https://jsbin.com/viziyewore/edit?js,console
```js
function callName() {
  console.log(this.name);
}

var name = '全域';
var obj = {
  name: '區域',
  callName: callName,
  watch: {
    name: 'Watch',
    callName: callName
  }
}
callName()   // "全域"
obj.callName(); //"區域" ，呼叫是在物件下調用，那麼 this 則是該物件
obj.watch.callName(); //"Watch"
```

https://jsbin.com/vihonezita/edit?js,console
```js
var name = '全域';
var obj = {
  name: '區域',
  callName: function() {
    console.log(this.name);
  }
}

//callName;   // callName is not defined
//callName();   // error" "TypeError: callName is not a function
obj.callName(); //"區域" ，呼叫是在物件下調用，那麼 this 則是該物件
var callName = obj.callName;
callName();  // "全域"
```

## 立即函式：

```js
var name = '全域';
(function() {
  function callSomeone() {
    console.log(this.name); 
  }
  callSomeone(); //"全域"
})();
```

```js
var name = '全域';
(function () {
  var name = '區域';
  console.log(this.name); //"全域"
})()
```

```js
var name = '全域';
var obj = {
  name: '區域',
  callName: function () {
    console.log(this.name);
  }
};
(function() {
  obj.callName(); // "區域"
})();
```

## Closure

https://jsbin.com/tagalenuje/edit?js,console
```js
var name = '全域'
function easyCard(base = 100) {
  var money = base
  return function(update = 10) {
    money = money + update
    console.log(this.name, money)
  }
}

var MingEasyCard = easyCard(100)
MingEasyCard(); // 110
MingEasyCard(); // 120

var YourEasyCard = easyCard(20);
YourEasyCard(); //30
var YourEasyCard2 = easyCard(20);
YourEasyCard2(100); // 120

var MyEasyCard = easyCard(1000)(100);
MyEasyCard(100);  // "TypeError: MyEasyCard is not a function
```


```js
var name = '全域'
function easyCard(base = 100) {
  var money = base
  var name = '悠遊卡'
  return function (update = 10) {
    money = money + update
    console.log(this.name, money) // "全域"  110
  }
}
var MingEasyCard = easyCard(100) 
MingEasyCard()

```

## Callback

```js
function myEasyCard(callback) {
  var money = 150
  return callback(money)
}
myEasyCard(function (money) {
  console.log( money + 100) //250
})
```

```js
var a = [1, 2, 3];
a.forEach(function(item) {
  console.log(this, item)
});
```
https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#語法
```js
arr.forEach(function callback(currentValue[, index[, array]]) {
    //your iterator
}[, thisArg]);
```
這個 callback 函式將會把 Array 中的每一個元素作為參數，帶進本 callback 函式裡，每個元素各執行一次，接收三個參數：  
currentValue 代表目前被處理中的 Array 之中的那個元素。 index,array, thisArg 選擇性

Note: IIFE、Closure、Callback function 與 this 關係是!? 沒有關係


## bind, apply, call 

JavaScript  Call 
[使用給定的this參數以及分別給定的參數來呼叫某個函數](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call)  

```js
function callName(name) {
  console.log(this.name, name);
}

var name = '全域';
var obj = {
  name: '區域',
}
callName(undefined, '全域2'); // "全域" undefined (this.name, name)
callName.call(undefined, '呼叫'); // "全域" "呼叫" (this.name, name)
callName.call(obj, '呼叫'); // "區域" "呼叫" (this.name, name)
```

bind 是ES5中新增的一個方法，可以改變函數內部的this指向


bind的應用場景  
借用Array的原生方法

https://jsbin.com/pupasabapa/edit?js,console
```js
var a = {};
Array.prototype.push.bind(a, "hello", "world")();

console.log(a); 
// [object Object] {
//   0: "hello",
//   1: "world",
//   length: 2
// }
```
http://www.dengzhr.com/js/1069




### 箭頭函式
> 「箭頭函式沒有自己的 this」

https://jsbin.com/wuxiqeciko/edit?js,console
```js
var name = '全域'
var obj = {
  name: '區域',
  callName: function () { 
    // 注意，這裡是 function，以此為基準產生一個作用域
    console.log('1', this.name); // 1 "區域"
    setTimeout(() => {
      console.log('2', this.name); // 2 "區域"
      //console.log('3', this); // 3 obj 這個物件
    }, 10);
  },
  callNameArrow: () => { 
    // 注意，如果使用箭頭函式，this 依然指向 window
    console.log('4', this.name); // 4 "全域"
    setTimeout(() => {
      console.log('5', this.name); // 5 "全域"
      //console.log('6', this); // 6 window 物件
    }, 10);
  }
}
obj.callName();
obj.callNameArrow();
```


`const func = (x) => x + 1`   
`const func = function (x) { return x + 1 }`
JS語言中函式的設計，必有回傳值，沒寫相當於回傳`undefined`    

#### References

https://wcc723.github.io/javascript/2019/03/18/JS-THIS/
https://paper.dropbox.com/doc/JSJavaScript-This---AZqD8PDvbl5uk5Mfq_EJlXMkAg-Xw50EZtMFNqG0wUxKeIaz
https://wcc723.github.io/javascript/2017/12/21/javascript-es6-arrow-function/