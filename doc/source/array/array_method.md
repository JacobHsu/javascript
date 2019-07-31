title: Array Method
---

### 一行代碼去重數組

[Set](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Set)  
```js
const list = [1, 1, 2, 3, 6, 45, 8, 5, 4, 6, 5]
const uniqueList = [...new Set(list)] // [1, 2, 3, 6, 45, 8, 5, 4]
console.log(uniqueList)
```