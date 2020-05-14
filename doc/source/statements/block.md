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
    function test(){}
    test = 123
    console.log('inner:',test) // inner: 123
}
console.log('outer:',test) // outer: ƒ test(){}
```
