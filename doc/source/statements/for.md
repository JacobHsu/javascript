# for…of與for…in的差別

[For...Of](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...of)

[for...in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)

> 提示：`for...in`不应该用于迭代一个 Array，其中`索引顺序`很重要。

在迭代**物件屬性**時，使用 `for...in`；在迭代**陣列**時，使用 `for...of`。
`for...in` 輸出的是屬`性名稱(key)`，`for...of` 輸出的是`值(value)`
`for...of` 是 ES6 的新語法。修復了ES5 `for…in` 的不足
`for...of` 不能迭代物件，需要透過和 `Object.keys()` 搭配使用

單純迭代陣列的話，for...in 輸出的是屬性名稱(key)，for...of 輸出的是值(value)

```js
let iterable = [3, 5, 7];

// 回傳「key」
for (let i in iterable) {
  console.log(i); // "0", "1", "2"
}

// 回傳「value」
for (let i of iterable) {
  console.log(i); // 3, 5, 7
}
```

在原本的陣列，新增一個屬性 foo，可看到 for...in 有將此屬性 foo 也輸出。

```js
let iterable = [3, 5, 7];
iterable.foo = 'hello';   //新增foo屬性名稱

// 回傳「key」，且會讀取到陣列新增的屬性名稱
for (let i in iterable) {
  console.log(i); // "0", "1", "2", "foo"
}

// 回傳「value」
for (let i of iterable) {
  console.log(i); // 3, 5, 7
}
```
