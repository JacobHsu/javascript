title: JavaScript 核心
---

## JavaScript 直譯器轉換過程

語法基本單元化(Tokenizing)  
抽象結構樹AST(Abstract Syntax Tree)  
代碼生成  


[esprima.org](https://esprima.org/demo/parse.html)  
> Parser produces the (beautiful) syntax tree  


### Lexical Scope 語法作用域 (靜態作用域)  
直譯器 靜態作用域 語法解析時就已經確定作用域 不會改變  JS屬於靜態作用域  
執行 動態作用域  作用域是函數調用時才決定     


# 提升（Hoisting）

在創造環境把記憶體空間準備好，這個流程稱為 提升（Hoisting）  

`var name = 'Jacob'` // 創造環境 name放入記憶體 name = undefined

```js
var name; //先宣告變數
name = 'Jacob' //然後才賦予值 執行階段  
```

**函數陳述式** 在創造階段就會**優先載入**  
> 創造階段函式已可以運行 


```js
var a = '1'
function fn() {
    ...
}
```

|    |             |   
|--- |-------------|
| a  | undefined   |   
| fn | function .. |   


```js
fn() //放前面可因為 創造階段 已可以運行
function fn() {
    console.log()
}
```


```js
fn() //放前面 uncaught typeError: fn is not a function 
console.log(fn) //undefined
var fn = function () { //函式表達式  
    console.log()
}
```

**創造階段函式優先**  
  
```js
//創造階段
function fn () {  
    console.log(1)
}

var fn;

//執行階段
fn = function () { 
    console.log(2)
}
console.log(fn) //2
```
