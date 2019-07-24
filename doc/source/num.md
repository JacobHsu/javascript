title: number
---

Math.pow()傳回指定乘冪數的基底運算式值

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