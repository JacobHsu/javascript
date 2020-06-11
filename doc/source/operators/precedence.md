
## [運算子優先序](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

```js
var s = 'msg'
console.log((s ==='msg') ? "something" : "nothing" )
console.log("value is " + (s ==='msg') ? "something" : "nothing" ) // something
```

value is 不見了  
`+` 優先序高於 `… ? … : …`  
`value is " + (s ==='msg')` // true

## .運算符比 = 運算符高

```js
var a = {n: 1}
var b = a
a.x = a = {n: 2}

console.log(a.n, b.n);
console.log(a.x, b.x);
```

2 1
undefined {n: 2}

```js
var b = a,此時a和b指向同一個對象。

.運算符比 = 運算符高,先計算`a.x`,此時 
b = {
    n:1,
    x:undefined
}

相當於給對象添加了x屬性。

a.x = a = {n:2};

計算完a.x,再計算 = ,賦值是從右向左,此時a指向一個新對象。
a = {
    n:2
}

a.x已經執行過了,此時對象的x屬性賦值為a,此時

對象 = {
    n:1,
    x:{
        n:2
    }
}

即:
a = {
    n:2
}

b = {
    n:1,
    x:{
        n:2
    }
}
```
