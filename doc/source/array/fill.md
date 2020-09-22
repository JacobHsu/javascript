title: Array fill
---

[fill](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

```js
const array1 = [1, 2, 3, 4];

// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]

// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]
```

`{1:200, 2:140, 5:400}`
請將上面的數據格式轉換為`[200, 140, null, null, 400, null, null, null, null, null, null, null]`,其中數組的長度為12

```js
const obj = { 1: 200, 2: 140, 5: 400 };
function translate(obj) {
  return Object.assign(Array(13).fill(null), obj).slice(1);
}
// 輸出 [200, 140, null, null, 400, null, null, null, null, null, null, null]
console.log(translate(obj));
```
