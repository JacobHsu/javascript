title: Array splice
---

## 分割指定长度的元素数组

```js
const listChunk = (list, size=1, cacheList=[]) => {
    const tmp = [...list]
    if(size <0) return list
    while(tmp.length) {
        cacheList.push( tmp.splice(0,size))
    }
    return cacheList
}
console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9])) // [[1], [2], [3], [4], [5], [6], [7], [8], [9]]
 console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], 3)) // [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
 console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], 0)) // []
 console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], -1)) // []
```
