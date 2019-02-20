title: Array Merge
---

### concat

合併陣列

[Array.prototype.concat()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

```js
var a = [1, 2, 3], b = [4, 5, 6];
var c = a.concat(b);
console.log(c); // 1,2,3,4,5,6
console.log(a); // 1,2,3 不改變本身
```

JS 中合併多個陣列，且去除陣列重複元素




```js
var a = ["a", "b", "c"],
    b = ["c", 1, 2];
var arr = a.concat(b);
console.log(arr); // ["a", "b", "c", "c", 1, 2]
```

要求必須返回原陣列  
https://jsbin.com/nidizam/edit?js,console
```js
// 對該陣列進行循環
arr.forEach((item, index) => {
  // 如果當前下標和當前元素在陣列中的lastIndex不同，則刪除這個元素
  if (index != arr.lastIndexOf(item)) {
    arr.splice(index, 1);
  }
});
console.log(arr); // "a", "b", "c", 1, 2]
```

要求返回新陣列  
https://jsbin.com/lufavuf/1/edit?js,console
```js
// 最簡單的應該是使用陣列的 filter 方法，將當前下標和當前元素在數組中的 lastIndex 相同的元素篩選出來
var arr2 = arr.filter((item,index) => 
    index ===arr.lastIndexOf(item)
);
console.log(arr); // ["a", "b", "c", "c", 1, 2]
console.log(arr2); // ["a", "b", "c", 1, 2]
```
