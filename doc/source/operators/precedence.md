
## [運算子優先序](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

```js
var s = 'msg'
console.log((s ==='msg') ? "something" : "nothing" )
console.log("value is " + (s ==='msg') ? "something" : "nothing" ) // something
```

value is 不見了  
`+` 優先序高於 `… ? … : …`  
`value is " + (s ==='msg')` // true