title: Asynchronous 
---

## 異步

https://jsbin.com/honidujame/edit?js,console
```js
console.log(1)

setTimeout(()=>{
   console.log(2);
},0)

console.log(3)

setTimeout(function() {
  console.log(4);
},0)

// 1 3 2 4 
```

https://jsbin.com/hipiruzoru/edit?js,console
```js
console.log(1);
setTimeout(function(){
   console.log('setTimeout')        
},0)
let promise = new Promise(function(resolve,reject){
  console.log(3)
  resolve(100)
}).then(function(data){
  console.log(100)
})
console.log(2);

// 1 3 2 100 "setTimeout"
```

```js
console.log(0)
let promise = new Promise((resolve, reject)=>{
  console.log(1);
  setTimeout(()=>{
    console.log(2);
    resolve();
  },0)
  console.log(3)
})

promise.then(res=>{
  console.log(100)
})
console.log(4)

// 0 1 3 4 2 100 
```

## setTimeout

`setTimeout()`函數是異步的


```js
for (var i = 0; i < 5; i++) {
 setTimeout(function() {
   console.log(i); // 5,5,5,5,5
 }, i*1000);
}
```


```js
for (var i = 0; i < 5; i++) {
 setTimeout(function() {
  console.log(new Date, i);
 }, 1000);
}
console.log(i); //5,-> 5,5,5,5,5
```
因為異步函數必須等主進程運行完畢才會運行，setTimeout()內部回調運行的時候，主進程已經運行完畢了，此時i=5，所以輸出5。

循環執行過程中，幾乎同時設置了 5 個定時器，一般情況下，這些定時器都會在 1 秒之後觸發，而循環完的輸出是立即執行的

即第 1 個 5 直接輸出，1 秒之後，輸出 5 個 5；


提示： `setTimeout()` 只執行 code 一次。如果要多次調用，請使用 setInterval() 或者讓 code 自身再次調用 setTimeout()。

> `setTimeout`的意思是傳遞一個函數，延遲一段時候把該函數添加到**隊列**當中，並不是立即執行；
所以說如果當前正在運行的代碼沒有運行完，即使延遲的時間已經過完，**該函數會等待到函數隊列中前面所有的函數運行完畢之後才會運行**；也就是說所有傳遞給setTimeout的回調方法都會在**整個環境下的所有代碼運行完畢之後執行**；

### 期望代碼的輸出變成：5 -> 0,1,2,3,4

1 用立即執行函數 `IIFE（Immediately Invoked Function Expression`：聲明即執行的函數表達式）加閉包
```js
for (var i = 0; i < 5; i++) {
  (function(j){ //j =i
    setTimeout(function() {
        console.log(new Date, j);
    }, 1000);
  })(i)
}
console.log(i); //5, 0,1,2,3,4
```
用立即執行函數表達式創造了新的函數作用域將timer函數包裹了起來，並用j捕獲了每次循環時的i ，這樣在運行到console.log(j)的時候顯示的就是每次循環時的i值


2 利用[API 文檔](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)

```js
for (var i = 0; i < 5; i++) {
    setTimeout(function(j) {
        console.log(new Date, j);
    }, 1000, i);
}
console.log(i); //5, 0,1,2,3,4
```


3 利用 JS 中基本類型（Primitive Type）的參數傳遞是`按值傳遞（Pass by Value）`的特徵

```js
var output = function (i) {
    setTimeout(function() {
        console.log(new Date, i);
    }, 1000);
};
for (var i = 0; i < 5; i++) {
    output(i);  // 這裡傳過去的 i 值被複製了
}
console.log(i); //5, 0,1,2,3,4
```
