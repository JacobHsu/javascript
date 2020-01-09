title: replace
---

[String.prototype.replace()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

```js
var str = 'x-x_';
var retArr = [];
str.replace(/(x_*)|(-)/g, function(match, p1, p2) {
  if (p1) { retArr.push({ on: true, length: p1.length }); }
  if (p2) { retArr.push({ on: false, length: 1 }); }
});

console.log(retArr);
```
