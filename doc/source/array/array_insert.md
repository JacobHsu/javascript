title: Array Insert
---

![js-array-operations](https://raw.githubusercontent.com/tooto1985/js-array-operations/master/main.jpg)  

immutable 的重要性，處理資料要注意有沒有改變到本身。
處理 array 用 `push、pop、shift、unshift、reserve、sort、splice` 都會改變原有的陣列。這個觀念在處理複雜的全域變數陣列有幫助。

## 把數據插入陣列尾部

利用陣列長度進行賦值  
```js
let arr = [1,2,3,4,5];
arr[arr.length] = 6;
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.push` 方法    
```js
let arr = [1, 2, 3, 4, 5];
arr.push(6);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.concat` 方法  
```js
let arr = [1, 2, 3, 4, 5];
arr = arr.concat(6);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `spread` 運算符  
```js
let arr = [1, 2, 3, 4, 5];
arr = [...arr, 6];
console.log(arr); // [1, 2, 3, 4, 5, 6]
```


## 把數據插入陣列頭部

利用 `Array.prototype.unshift` 方法

```js
let arr = [1,2,3,4,5];
arr.unshift(0);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.concat` 方法

```js
let arr = [1,2,3,4,5];
arr.unshift(0);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `spread` 運算符
```js
let arr = [1, 2, 3, 4, 5];
arr = [0, ...arr];
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

## 把數據插入陣列指定位置

利用 `Array.prototype.splice` 方法

```js
let items = [1, 2, 4, 5];
items.splice(items.length / 2, 0, 3);
console.log(items);
```

## 拼接兩個陣列

利用 `Array.prototype.concat` 方法

```js
let arr = [1,2,3,4,5];
arr = [-2, -1, 0].concat(arr); 
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5]
```

利用 `spread` 運算符
```js
let arr = [1,2,3,4,5];
arr = [...[-2, -1, 0], ...arr];
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5]  
```

## example

[unshift](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) 把數據插入陣列頭部

下拉選單補標題　　　　
```js
const opts = this.dataOpts.map(data => ({
    value: data.id,
    text: data.name
}))
opts.unshift({
    value: null,
    text: 'select_title'
})
```