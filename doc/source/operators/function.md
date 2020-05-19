
# [函數表達式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/function)

函數表達式（function expression）非常類似於函數聲明（function statement）（詳情查看函數聲明），並且兩者擁有幾乎相同的語法。函數表達式與函數聲明的最主要區別是函數名稱（function name），在函數表達式中可省略它，從而創建匿名函數（anonymous functions）。

```js
// 函數聲明
function name([param[, param[, ... param]]]) { statements }
// 函數表達式
var myFunction = function name([param[, param[, ... param]]]) { statements }
// 函數表達式 匿名函數
var myFunction = function([param[, param[, ... param]]]) { statements }
```

```js
(function(){
    debugger
})()
```

函數表達式提升 (Function expression hoisting)

JavaScript中的函數表達式沒有提升,不像函數聲明,你在定義函數表達式之前不能使用函數表達式:

```js
notHoisted(); // TypeError: notHoisted is not a function

var notHoisted = function() {
   console.log('bar');
};
```


