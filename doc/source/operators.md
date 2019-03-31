title: Operators
---

## What is the difference between the equality operators `==` and `===`?

三個等號 `===` 表示嚴格相等，也就是說類型和值都必須相同。兩個等號 `==` 會使其中一邊的類型進行強制轉換，使等號兩邊的類型都相等後再對數值進行比較。

**加分回答**   

儘量使用全等操作符。因為其沒有隱式轉換，這樣結果會比較容易預測、計算也會比較快


除了等於操作符，還可以使用 `Object.is` 進行同值比較。他有著自己的特殊用途，不應說他更寬鬆或更嚴格於其他等於操作符


`===` 比較不是一個比較好的解決方式，你可以得到這樣的結果：

`NaN === NaN //false`  

好消息是在 ES6 有一個新的 `Object.is()`，它是更精確而且和 `=== `有相同的功能，在某些特殊情況下也運作的很好：

Mozilla 團隊 不認為 Object.is 比 === 更嚴格，他們宣稱我們應該思考這些方法如何處理 `NaN、-0 和 +0`  
```js
Object.is(0 , ' '); //false
Object.is(null, undefined); //false
Object.is([1], true); //false
Object.is(NaN, NaN); //true
```

https://jsbin.com/guqetaviho/edit?js,console

```js
var a = true, b = 1;

console.log(a==b); //true
console.log(a===b); //false

console.log(a==b==1); //true
console.log(a===b==1); //false
console.log(a===b===1); //false 
console.log(a==b===1); // false

console.log(a==b==0); // false
console.log(a===b==0); // true
console.log(a===b===0); // false
console.log(a==b===0); // false
```



http://www.jstips.co/zh_tw/javascript/why-you-should-use-Object.is()-in-equality-comparison/
https://30secondsofinterviews.org/  
https://hacpai.com/article/1546570870626?r=Vanessa  

## ++	Increment

後置遞增 `i++` 和前置遞增 `++i` 操作有什麼區別？  

他們都會使變量增加 1，只是計算和賦值的順序不一樣。

後置遞增是先賦值後計算，如：
```js
let i = 1;
console.log(i); //  1
let a = i++;
console.log(i); //  2
console.log(a); //  1
```
前置遞增是先計算後賦值，如：
```js
let i = 1;
console.log(i); //  1
let a = ++i;
console.log(i); //  2
console.log(a); //  2
```


https://jsbin.com/samaxubazo/edit?js,console  
```js
function aFunc(x) {
  return () => console.log(x++);
}
function bFunc(x) {
  return x++;
}
function cFunc(x) {
  return ++x;
}
let newFunc = aFunc(1)
newFunc() //1
newFunc() //2
newFunc() //3

console.log(bFunc(1)) //1
console.log(cFunc(1)) //2
```

references
===
https://www.w3schools.com/js/js_operators.asp
https://hacpai.com/article/1546665384680?r=Vanessa  


## Adding Strings and Numbers

```js
var x = 5 + 5; // 10
var y = "5" + 5; // 55
var z = "Hello" + 5; //Hello5
```

https://jsbin.com/hupumaxoru/edit?js,console
```js
console.log(1+"2"+"2"); // "122"
//console.log(1++"2"+"2"); // "error"  "ReferenceError: Invalid left-hand side expression in postfix operation
console.log(1+ +"2"+"2"); // "32"
console.log(1+ -"1"+"2"); // "02"
console.log(+"1"+ +"1"+"2"); // "22"
console.log("A"-"B"); // NaN
console.log("A"-"B"+"2"); // "NaN2"
console.log("A"+"B"+"2");  // "AB2"
console.log("A"+"B"+2);  //  "AB2"
```

https://www.w3schools.com/js/js_operators.asp

