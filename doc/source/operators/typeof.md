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

## null

`[typeof null, null instanceof Object]` // ["object", false]
js 萬物即對象 但null不是Object new出來的

ref: [instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)

Object.prototype.name = 1 ;  
`1.0.name;` // 1  1是整型 1.0 變對象     
`1.name;` // Uncaught SyntaxError: Invalid or unexpected token js沒有整型只有對象  
`Function.name;` // "Function"  