# let

`let` 用於宣告一個「只作用在當前區塊的變數」，初始值可選擇性的設定。

```js
var a = 1;
if(true){
    console.log(a);
    let a = 2;
}
```

ReferenceError: Cannot access 'a' before initialization
`let`聲明的變量不會提升,並且會產生暫存死區。在`let`聲明變量之前訪問變量會拋出錯誤。