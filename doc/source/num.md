title: number
---

## 取值 

Math.pow()傳回指定乘冪數的基底運算式值

`console.log( Math.pow(10, 3) ); // 1000`

[Math.round()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/round) 函數回傳四捨五入後的近似值  

[Math.floor()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) 函式會回傳無條件捨去後的最大整數  

[Math.ceil()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil) 函式會回傳大於等於所給數字的最小整數 


```js
export function precisionRound(number, precision) {
  const factor = Math.pow(10, precision)
  return Math.round(number * factor) / factor
}

export function precisionFloor(number, precision) {
  const factor = Math.pow(10, precision)
  return Math.floor(number * factor) / factor
}

export function precisionCeil(number, precision) {
  const factor = Math.pow(10, precision)
  return Math.ceil(number * factor) / factor
}
```

 ## 補數字

 [JavaScript 数字前补“0”的五种方法](https://blog.csdn.net/chy555chy/article/details/62886715)  

數字補0  

 ```js
//轉為小數
function padding3(num, length) {
    var decimal = num / Math.pow(10, length);
    //toFixed指定保留幾位小數
    decimal = decimal.toFixed(length) + "";
    return decimal.substr(decimal.indexOf(".")+1);
}
console.log( padding3(7,3) ) //"007"

function padding4(num, length) {
    //這裡用slice和substr均可
    return (Array(length).join("0") + num).slice(-length);
  }
console.log( padding4(7,3) ) //"007"
 ```

 數字填充9

 ```js
function paddingPoint(length) {
    var decimal = 1 / Math.pow(10, length);
    decimal = decimal.toFixed(length) + "";
    return 1-decimal;
}
console.log( paddingPoint(3) ) // 0.999

function paddingInt(length) {
  return (Array(length).join("9") + 9).slice(-length);
}
console.log( paddingInt(3) ) //"999"

console.log( Number(paddingInt(3)) + paddingPoint(3) ) // 999.999
 ``` 