title: Date
---

[Date](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Date)

建立 Date 物件的方式：

```js
var today = new Date();
var birthday = new Date('December 17, 1995 03:24:00');
var birthday = new Date('1995-12-17T03:24:00');
var birthday = new Date(1995, 11, 17);
var birthday = new Date(1995, 11, 17, 3, 24, 0);
```

## Date.prototype.toISOString()

國際標準[ISO 8601](https://zh.wikipedia.org/wiki/ISO_8601)，是國際標準化組織的日期和時間的表示方法

```js
const d = new Date();
const today = d.toISOString().substring(0, 10);
console.log(today) //  "yyyy-mm-dd" format. 2020-05-25

let sevenDaysAgo = d.setDate(d.getDate() - 7);
sevenDaysAgo = new Date(sevenDaysAgo).toISOString().substring(0, 10);;
console.log(sevenDaysAgo) // 2020-05-18
```
