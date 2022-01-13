
# 空值合并操作符（??）

[Nullish coalescing operator](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) (??)

空值合并操作符（??）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。


```js
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
```



以前，如果想为一个变量赋默认值，通常的做法是使用逻辑或操作符（`||`）：
然而，由于 || 是一个布尔逻辑运算符，左侧的操作数会被强制转换成布尔值用于求值。任何假值（`0， ''， NaN， null， undefined`）都不会被返回。这导致如果你使用0，''或NaN作为有效值，就会出现不可预料的后果。

```js
let count = 0;
let text = "";

let qty = count || 42;
let message = text || "hi!";
console.log(qty);     // 42，而不是 0
console.log(message); // "hi!"，而不是 ""
```
