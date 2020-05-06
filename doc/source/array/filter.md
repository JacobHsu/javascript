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
