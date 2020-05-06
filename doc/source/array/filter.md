title: Array filter
---

[filter](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

```js
var arr = [0,1,2]
arr[10] = 10;
const result = arr.filter(function(x){
  return x === undefined;
})
console.log(result) // []
```
filter 和 map 基本屬性 會把 或直接略過那些空的東西 不處理

## ['1', '2', '3'].filter(parseInt) ?

> `filter` 为数组中的每个元素调用一次 callback 函数，并利用所有使得 callback 返回 true 或等价于 true 的值的元素创建一个新数组。

```js
parseInt('1', 0); // 1
parseInt('2', 1); // 不返回
parseInt('3', 2); // NaN 不返回
```

parseInt('1', 0)：radix的值為0，判斷字符串發現介於1~9，用10進制轉換，結果為1，所以callback的結果等價於true，返回元素'1'。

parseInt('2', 1)：radix的值為1，如果該參數小於 2 或者大於 36，則 parseInt() 將返回 NaN，結果不等價於true，不返回。

parseInt('3', 2): radix的值為2，這就意味著字符串將被解析成字節數，也就是僅僅包含數值0和1。parseInt的規範指出，它僅嘗試分析第一個字符的左側。這個字符串的第一個字符是“3”，它並不是基礎基數2的一個有效數字。所以這個子字符串將被解析為空。如果子字符串被解析成空了，函數將返回為NaN。

https://juejin.im/post/5dbff8735188252ddb2fd25e

`['1', '2', '3'].filter(parseInt) //  ["1"]`
