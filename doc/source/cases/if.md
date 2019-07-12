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
