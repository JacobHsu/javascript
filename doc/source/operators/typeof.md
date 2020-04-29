# typeof

```js
var f = function g() {
    return 123
}
typeof g(); // Uncaught ReferenceError: g is not defined
typeof f; // "function"
```

g() 不能變動 變量 f `function_expression` 可以重新賦值
g() 只能在函數內使用 外部無法存取

```js
// g() 函數聲明
function g() {
    return 123
}
typeof g(); // "number"
```

ref [函數](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions)