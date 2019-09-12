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

程式
```js
function fn () {  
    console.log(a)
}
var a = 'hello'
fn()
```

實際運作拆解
```js
//創造階段
function fn() {  
    console.log(a)
}
var a;
//執行階段
a = 'hello'
fn () 
```

```js
function fn() {
    if(a) { // undefined 在 JavaScript 代表著 false
        console.log('hello')
    } else {
        console.log('jacob')
    }
}
fn() //因為函式在執行時，變數還沒有被賦予值
var a = true
```


# 同步/非同步

JS是單執行序 是同步的  
可利用 `事件佇列` 實現非同步  同步概念的先跑完 非同步行為先移至事件佇列  

```js
setTimeout(function(){
    console.log('someone call')
},3000) //不管如何調整秒數 都不會優先執行  0也是最後執行  
```

# LHS  
`1= true`
1 = true 會出現 left-hand side (LHS)，實際上在此就無法繼續執行
`Uncaught ReferenceError: Invalid left-hand side in assignment` 

`console.log(a)`  
not defined 但其實是 RHS 錯誤，只是 JavaScript 並不會直接顯示 RHS 錯誤

# 陳述式 表達式  

[陳述式與宣告分類](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements)  
[運算式與運算子](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators)  
[正規表達式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Regular_Expressions)  

陳述式 不會回傳結果  
```js
// expression
100 + 100
// statement
var foo;
if(1==1) {}

// 物件實字  
var a = {
    name : "Jacob"
}
```

# 立即函式

(匿名函式())  //  匿名函式 外層小括號包起來  並且在後面加入() 來立即執行函式  
```js
(function(){
    console.log('Jacob')
}())
```

# ASI  自動分號插入

自動分號插入(`automatic semicolon insertion, ASI`) 是一種程序解析技術，
它在JavaScript 程序的語法分析(parsing) 階段起作用。

“不會” 發生 ASI 的規則：

1. 新的一行是 `(`、`[`、`/` 開始 (容易出錯的地方)  
2. 新的一行以 `+`、`-`、`*`、`%` 作開始 (會影響執行結果)    
3. 新的一行以 `,`、`.` 作開始 (需注意執行結果)  

遇到以上的標點符號**前方加入分號**是解決辦法    

```js
// 執行錯誤
(function() { })()
(function() { })()
 
// 正確
;(function() { })()
;(function() { })()
```

# 動態型別


```js
//執行階段才會賦予確立型別
var myName = 'Jacob'
var myName; // 先賦予命名空間
myName = 'Jacob' //執行階段才確認型別

console.log(typeof myName)
console.log(typeof 'Jacob')

//顯性的轉換 explicit conversion
//隱性的轉換 implicit conversion
var num = 1 //number  
num = num + '' //string  
num = num * 3 //number  
console.log(num, typeof num)
```

# 原始型別及物件型別

原始型別 可用包裹物件的所有方法  
```js
a = 'Jacob'
var e = new String(a) //但是原始型別盡量不用此方式 建構式 宣告 
console.log(a, e) 
console.log(typeof e) // 建構式宣告的非原始型別 是物件型別  
```

# 運算子

[運算子](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators)  
[運算子優先序](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)  

賦值的優先性很低只有3 `Assignment`  

`console.log(1<2<3); //true`  
`console.log(3>2>1); //false`  

`console.log(3>2) // true`  
`console.log(1>1) // false`  

a = b = 3 // a是收 3賦予至b的 '回傳結果' 

```js
const b = {};
Object.defineProperty(b, 'a', {
    value: 2,
    writable: false
})

b.a = 3
console.log(b.a) //2

var a = 3;  
a = b.a = 1;  
console.log(a, b.a) // 1, 2  

// b.a 是表達式 接收 1  b.a = 1 跟 b.a沒有關連性

```

