# split

[String.prototype.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)

> 請輸出1到400之間所有數字中包含的1的個數，比如數字1中包含了一個1, 數字11中包含了兩個1,數字20中不包含1,數字1到21中共包含了13個1。

將每一個數字轉換為字符串然後統計`1`的個數

```js
function getCount() {
  let count = 0
  for(let i=1;i<400;i++) {
    count = count + `${i}`.split('1').length - 1
  }
  return count
}

// 輸出 180
console.log(getCount())
```
