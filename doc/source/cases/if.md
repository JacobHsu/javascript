title: if else
---


good programming patterns  

三元運算符

[Nested ternaries](https://www.johnstewart.dev/five-programming-patterns-i-like/)  

```js
let result = null;
if (conditionA) {
  if (conditionB) {
    result = "A & B";
  } else {
    result = "A";
  }
} else {
  result = "Not A";
}

const result = !conditionA
  ? "Not A"
  : conditionB
  ? "A & B"
  : "A";
```


```js
var a = [0]
if(a) {
  console.log( a == true)
} else {
  console.log("done")
}
```

if 作為判斷數組有東西會過 但js怕比 `[0] == true` false
