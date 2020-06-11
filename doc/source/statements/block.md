title: 區塊
---

區塊陳述用來組合零個或多個陳述。我們使用一對大括號 { } 以界定區塊。

var

```js
var x = 1;
{
  var x = 2;
}
alert(x); // outputs 2
```

let 和 const

```js
let x = 1;
{
  let x = 2;
}
console.log(x); // logs 1
```

function

```js
function foo() {
    {
        var a = 'var';
        {
            let a = 'let';
            console.log(a);  // let
        }
    }
    console.log(a);  // var
}
foo();
```

```js
{
    debugger
    function test(){}
    test = 123
    console.log('inner:',test) // inner: 123
}
console.log('outer:',test) // outer: ƒ test(){}
```

塊會限制函數的提升

有条件的创建函数

[函数可以被有条件来声明](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/function)，这意味着，函数声明可能出现在一个 if 语句里，但是，这种声明方式在不同的浏览器里可能有不同的效果。因此，不应该在生成环境代码中使用这种声明方式，应该使用函数表达式来代替。

```js
var hoisted = "foo" in this;
console.log(`'foo' name ${hoisted ? "is" : "is not"} hoisted. typeof foo is ${typeof foo}`);
if (false) {
  function foo(){ return 1; }
}

// 在Chrome里: 
// 'foo' 变量名被提升，但是 typeof foo 为 undefined
// 
// 在Firefox里:
// 'foo' 变量名被提升. 但是 typeof foo 为 undefined
//
// 在Edge里:
// 'foo' 变量名未被提升. 而且 typeof foo 为 undefined
// 
// 在Safari里:
// 'foo' 变量名被提升. 而且 typeof foo 为 function
```

`var`不會產生塊級作用域,`let`會產生塊級作用域。

```js
if(false){
    var a = 1;
    let b = 2;
}
console.log(a); 
console.log(b); 
```

代碼相當於:
```js
var a;
if(false){
    a = 1;
    let b = 2;
}
console.log(a); // undefined
console.log(b); // ReferenceError: b is not defined
```