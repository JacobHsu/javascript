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


```js
var name = '全域'
var obj = {
  //name : '物件的',
  x: function() {
    name = '函式的';
    console.log(this.name); //"物件的"  找不到就會undefined
  }
}
obj.x()
```

```js
var name = '全域'
var obj = {
  n: function() {
    var name = '新函式的';   
    setTimeout(function(){
      console.log(this.name) // '全域'
    },0)
  }
}
obj.n()
```

```js
var name = '全域'
var obj = {
  //name : '物件的',
  x: function() {
    name = '函式的';  
    setTimeout(function(){
      console.log(this.name) // '函式的'
    },0)
  }
  n: function() {
    var name = '新函式的';   
    setTimeout(function(){
      console.log(this.name) // '函式的'
    },0)
  }
}
obj.x()
obj.n()
```

## 簡易呼叫

```js
var name = '全域'
var obj = {
  name : '物件的',
  getName: function() {
    return this.name;
  }
}
var getName = obj.getName;
console.log(getName()) //"全域"
```

```js
var name = '全域'
var obj = {
  name : '物件的',
  fn: function(a, b, c) {
    return this.name+','+a+','+b+','+c;
  }
}
var fnA = obj.fn;
var fnB = fnA.bind(null, 0); // a
console.log( fnB(1, 2) ) // b c   "全域,0,1,2"
```

```js
var name = '全域'
var obj = {
  name : '物件的',
  fn: function(a, b, c) {
    'use strict'
    return this+','+a+','+b+','+c;
  }
}
var fnA = obj.fn;
var fnB = fnA.bind(null, 0); // a
console.log( fnB(1, 2) ) // b c   "null,0,1,2"
```

```js
var value = 'global';
var foo = {
  value: 'local',
  bar: function() {
    return this.value;
  }
}
console.log(foo.bar()); // "local"
// 下面是表達式 執行時直接把函數取出來 執行函式的結果
console.log( foo.bar = foo.bar ); // function() {return this.value;}
// 賦值是表達式 表達式會回傳結果  
console.log( (foo.bar = foo.bar)() ); // "global" 
console.log( (false || foo.bar)() ) // "global"
```

```js
var value = 'global';
var obj = {
  x: function() {
    value: 'fn',
    console.log(this.value); //undefined
  },
}
obj.x(); // "local"
```

```js
var value = 'global';
var obj = {
  
  x: function() {
    value: 'fn',
    console.log(this.value);
  },
  value: 'local',
}
obj.x(); // "local"
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

`call & apply` 可以作為呼叫 Function 的另一個手段，皆是回傳function執行結果
而 `bind` 則會回傳一個經過包裹後的 Function 回來，回傳的是綁定 this 後的*原函數*。
> 「綁定this的函數」 一但被綁定，其this無法再被修改。

call vs. apply 作用完全一樣，只是接受參數的方式不太一樣
```js
func.call(this, arg1, arg2);
func.apply(this, [arg1, arg2]); //陣列
```

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
callName.call(undefined, '呼叫'); // "全域" "呼叫" (this.name, name) 無值傳入this往上找
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

### map

```js
// ['1','2','3'] 字串透過parseInt 轉數字
var arr = ['1','2','3'].map(parseInt);
console.log(arr) // [1, NaN, NaN]

var arr = ['1','2','3'].map(function(item, i){
  console.log(item, i) // parseInt('1', 0);  parseInt('2', 1);  parseInt('3', 2);
  // parseInt('2', 1) 進位系統的1 表數字到1 進到下一位 所以2不會存在NaN  
  // parseInt('11', 2) 進位系統的2 11表示2+1=3
  return parseInt(item, 10) // "1" "2" "3"  parseInt(item, i)
});
```
[map()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map)   callback 回呼函式  參數 currentValue index array  
[parseInt()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/parseInt) radix 能代表該進位系統的數字  注意，通常預設值不是 10 進位

#### References

https://wcc723.github.io/javascript/2019/03/18/JS-THIS/
https://paper.dropbox.com/doc/JSJavaScript-This---AZqD8PDvbl5uk5Mfq_EJlXMkAg-Xw50EZtMFNqG0wUxKeIaz
https://wcc723.github.io/javascript/2017/12/21/javascript-es6-arrow-function/