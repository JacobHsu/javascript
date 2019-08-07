title: 箭頭函式
---

## Arrow Function


[什麼時候不使用箭頭函數](https://juejin.im/post/5d4770ecf265da03dd3d5642?utm_source=gold_browser_extension)  


###　定義對象上的方法

```js
const calculate = {
  array: [1, 2, 3],
  sum: () => {
    console.log(this === window); // => true
    return this.array.reduce((result, item) => result + item);
  }
};
console.log(this === window); // => true
// Throws "TypeError: Cannot read property 'reduce' of undefined"
calculate.sum();
```

是因為箭頭函數按詞法 **作用域將上下文綁定到 window 對象**  
執行`this.array`等同於`window.array`，它是`undefined`。


解決方法是使用**常規函數表達式**來定義方法。 
this 是在調用時確定的，而不是由封閉的上下文決定的


```js
const calculate = {  
  array: [1, 2, 3],
  sum() {
    console.log(this === window); // => false
    console.log(this === calculate); // => true
    return this.array.reduce((result, item) => result + item);
  }
};
calculate.sum(); // => 6
```

因为sum是常规函数，所以在調用 `calculate.sum()` 時 this 是 `calculate 對象`。 `this.array`是數組引用