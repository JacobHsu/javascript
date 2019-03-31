title: Scope
---

變數的作用域在函式內  
全域變數 vs 區域變數：內可用外，外不可用內。
不能污染全域變數。


```js
var value = "global";
var fn = function() {
  console.log(value); // "global"
}
fn();
```

```js
var value = "global";
var fn = function() {
  console.log(value); // "global"
  value = "local";
  console.log(value); // "local"
}
fn();
```

```js
var value = "global";
var fn = function() {
  console.log(value); // undefined
  var value = "local";
}
fn();
```

```js
var scope = 'global';
function checkScope(){
    var scope = 'local';
    function fn(){
        return scope;
    }
    return fn();
};
console.log( checkScope() ); // "local"
```

```js
var value = 'global';

var person = {
  value: 'local',
  callSomeone: function() {
    console.log(value)
  },
}
person.callSomeone() //"global"
```

```js
var foo = "global";
(function(){
  var bar = "Local"
  console.log(foo+bar); //"globalLocal"
})();
console.log(foo+bar); // "error" ReferenceError: bar is not defined
```


```js
(function() {
   var a = b = 1;
})();

console.log(b); // 1  b沒有宣告 為全域
```
'use strict'  
```js
(function() {
  'use strict';
  var a = b = 1;
})();
console.log(b); // "error"  "ReferenceError: b is not defined
```
注意: 只有將 `'use strict'` 放在函式開頭才會有作用。


### References
https://paper.dropbox.com/doc/JS--AaILvqN7Gcen3zEExnLuHUzmAg-K98zBcemd1Ig9DZYYNruL
https://wcc723.github.io/javascript/2017/12/15/javascript-use-strict/