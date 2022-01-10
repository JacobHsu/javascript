title: Variable
---

JavaScript的數據類型

JavaScript一共有8種數據類型
其中有7種基本數據類型：

ES5的5種：`Null`，`undefined`，`Boolean`，`Number`，`String`，

ES6新增：`Symbol` 表示獨一無二的值

ES10新增：`BigInt` 表示任意大的整數

一種引用數據類型：

`Object`（本質上是由一組無序的鍵值對組成）

包含function,Array,Date等。JavaScript不支持創建任何自定義類型的數據，也就是說JavaScript中所有值的類型都是上面8中之一。


```js

var name = 'Jacob';
console.log(window.name); //"Jacob"

mom = 'Jacob';
console.log(window.name); //"Jacob"

(function () {
  name = 'Jacob'
})();
console.log(window.name); //"Jacob"
```

宣告的變數不能被刪除 屬性可以被刪除
```js
var name1 = "Jacob1";
name2 = "Jacob2"; 
(function () {
  name3 = "Jacob3"; 
})();
delete name1;
delete name2;
delete name3;
console.log(window.name1); //"Jacob1"
console.log(window.name2); // undefined
console.log(window.name3); // undefined
```


## 變數的作用域在函式內

```js
  var value1 = "global";
  var class1 = {
    value2: "local",
    function1 :function() {
      var value3 = "function";
    }
  }
  
 console.log(value1); //"global"
 console.log(class1.value2); //"local"
 console.log(class1.value3); //undefined
```


```js
var value = 1;

function foo() {
  console.log(value); // 1
}

function bar() {
  var value = 2;
  foo();
}

bar();
```






## Hoisting

函式會自動提升

```js
callSomeone('Jacob'); // "打給 Jacob"
function callSomeone(name) {
  console.log('打給 ' + name)
}
```

變數會自動被提升
```js
console.log(myname); // "error" ReferenceError: myname is not defined
```

```js
console.log(myname); // undefined
var myname = 'jacob';
```

```js
fn()
function fn(params) {
  console.log(a) // undefined
  if (a) {
    a = 2;
  }
  console.log(a) // undefined
}
var a = 1;
console.log(a) // 1
```

```js
fn()
function fn(params) {
  console.log(a) // undefined
  if (! a) {
    a = 2;
  }
  console.log(a) // 2
}
var a = 1;
console.log(a) // 1
```


```js
fn();
function fn() {
  console.log(a); // undefined
}
var a = 1;
```

```js
function foo() {
    console.log('1');
}
foo(); // 第一次執行 "2"

function foo() {
    console.log('2');
}
foo(); // 第二次執行 "2"
```

## 動態型別
```js
var a = '1';
console.log(typeof a) // "string"
a = +a;
console.log(typeof a) // "number"
a = a + '';
console.log(typeof a) // "string"
```

```js
console.log(100 === '10' * 10) // true   '10' * 10 => number
```

https://paper.dropbox.com/doc/JavaScript--AaHkVSbD5F40g8SUfOv1i9ehAg-K98zBcemd1Ig9DZYYNruL