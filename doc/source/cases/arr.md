title: arrays
---

[一个合格的中级前端工程师必须要掌握的 28 个 JavaScript 技巧](https://juejin.im/post/5cef46226fb9a07eaf2b7516#heading-24)  


###　[One loop two arrays](https://www.johnstewart.dev/five-programming-patterns-i-like/)

https://jsbin.com/janoyunemu/edit?js,console

```js
const exampleValues = [2, 15, 8, 23, 1, 32];
const [truthyValues, falseyValues] = exampleValues.reduce((arrays, exampleValue) => {
  if (exampleValue > 10) {
    arrays[0].push(exampleValue);
    return arrays;
  }

  arrays[1].push(exampleValue);
  return arrays;
}, [[], []]);

console.log(truthyValues); // [15, 23, 32]

console.log(falseyValues); // [2, 8, 1] 
```

## 如何快速將一個字符串數組轉化為數字類型的數組

```js
['1', '2', '3'].map(parseFloat)
['1', '2', '3'].map(Number)
```

[['1', '2', '3'].map(parseInt)的輸出結果是什麼？](https://juejin.im/post/5dbff8735188252ddb2fd25e?utm_source=gold_browser_extension)  