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

```js
var a = 1
(function(){
    console.log(a);
})()
// var a = 1(function(){ console.log(a);})()
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

凡是使用 `new` 所建構的型別，在 typeof 都會是 `object`
透過建構式來建立的物件，`var a = new Object(); if(a)` 一樣是會被判定 true，因為物件的記憶體已經存在了


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

[Operators/Operator_Precedence](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)  

```js
var a = 10;
console.log(++a*a) //a + 1   11*11 121
var a = 10;
console.log(--a*a) //9*9 81
```

```js
var a = 1, b =2, c= 0;  
console.log(c || c && c || a)  
// 	Logical AND 6  	  Logical OR 5  從左至右
console.log(c || 0 && 0 || a)  
console.log(c || 0 || a)  
console.log(0 || 0 || a)  
console.log(0|| a)  
console.log(0|| 1)  
console.log(1)  
```

```js
var a = 1 + 1 === 1  
console.log(a = 2 === 1)  
console.log(false)  

1000 < 10000 < 10
console.log(true < 10)   
console.log(1 < 10)   
console.log(true)   
```


```js
var a = '1'; var b = 2;
var c = (a>b) ? a*b : sum(a,b);
function sum(a, b) {return a+b}

console.log('1'>2) 
console.log(1>2)  // ture
sum(a,b)
console.log('1'+2) //12  string型別相加  
console.log(c))  
console.log(12) 
```

# 嚴格相等 寬鬆相等  
```js
console.log(1) //數字1 藍色
console.log('1') //字串1  黑色

//嚴格相等 特殊狀況
console.log(NaN === NaN) //false 
console.log(+0 === -0) //true

//寬鬆相等
console.log(1 == '1') // true 布林和字串轉為數值
console.log(Number('1'))  

console.log(Number('0x11')) //17 0x是指十六進制數  16+1
console.log(17=='0x11') //true  

//Null Undefined 不會轉數字型別  
console.log(Number(null)) //0
console.log(Number(undefined))  //NaM 
console.log( null == undefined) //true
console.log( null === undefined) //false  

// 物件與非物件 使用包裹物件轉換 (Number String)
console.log([10])
console.log(10 == [10]) // [10] Number([10]) 10

console.log( {A:'A'}) //__proto__: Object  
console.log( String({A:'A'})) // [object Object]

//物件與物件 比對的不是值 是參考位址 參考同一個記憶體  
console.log( {}=={} ) //false  物件的參考位址不同
console.log( []==[] ) //false 同樣是物件型別  比對的都是參考位址

var a = [] 
var b = a ;//b取得的是a的參考位址
console.log( a===b) //a,b使用同個參考位址
```

[JavaScript Equality Table](https://dorey.github.io/JavaScript-Equality-Table/)  

# Truthy

[Truthy（真值）](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)

`console.log(new Boolean(false)) //Boolean{false} 物件`  __proto__: Object 

```js
if(new Boolean(false)) {
    console.log('Truthy')
} else {
    console.log('Falsy')
}
```

# 邏輯運算子及函式預設值

```js
console.log(1 && 2) //2
console.log(![]) //false

// 預設值為 0 的解決方法 使用三元運算子
// 當 cash 是數值或為 0 時，使用 cash 的數值
// 如果 cash 是 NaN 時，則直接套用 500
cash = (cash || cash === 0)? cash: 500; // or 左右兩邊放的是表達式
```  

# 物件取值

[求值策略](https://zh.wikipedia.org/wiki/求值策略)  

點 與 中括弧(可用變數方式)
物件取值屬性用字串
```js
const family = {
    name: 'Hsu',
    members: {
        mon: 'mon',
        dad: 'dad'
    },
    others: 'others',
    1: 10,
    '$-myFamily': 'my family',
    callFamily: function() {
        console.log('call family')
    },
    'Hello': function() {
        console.log('I am groot ')
    }
} //物件實字

console.log(family.name);
console.log(family['name']);
const a = 'name';
console.log(family[a]);

console.log(family[1]) //OK
console.log(family.1) //FAIL

family.callFamily();
family['callFamily']();

//add 
family['$'] = 'money'  
delete family.others
delete family['$']


//利用陣列及for迴圈 執行物件的函式
var familyMethod = ['callFamily','Hello']
for(var i=0; i< familyMethod.length;i++) {
    console.log(familyMethod[i])
    family[familyMethod[i]]();
}
```

```js
//變數無法被刪除，屬性才可以
var a=1;//變數
b=2; //屬性
console.log(window)
delete a;
delete b; //b is not defind
console.log(window)
```
## 物件記憶體空間

```js
var person = {
    name: 'Jacob'
}
var person2 = person
person2 = 'Hsu' //find 0x01 change name's value
```

| 參考物件   | Value   |
| ---------- | --------|
| 0x01       |         |
| name       | Jacob   |

| 物件變數   | Value   |
| ---------- | --------|
| person     | 0x01    |
| person2    | 0x01    |


```js
// 見大括號 生成新的參考物件  
var company = {
    team: 'dev',
    member: {
        rd: 'Jacob'
        qa: 'Claire'
    }
}
```

| 參考物件   | Value   |
| ---------- | --------|
| 0x01       |         |
| team       | dev     |
| member     | 0x02    |

| 0x02       |         |
| rd         | Jacob   |
| qa         | Claire  |

| 物件變數   | Value   |
| ---------- | --------|
| company    | 0x01    |


# 純值無法新增屬性

js兩種型別 不是純值 就是物件 (function是物件) 
```js
var newStr = 'myname' //純值
newStr.name = 'Jacob'
console.log(newStr)

var newStr2 = new String('myname') //建構式 物件
newStr2.name = 'Jacob'
console.log(newStr2)

function callFn() {
    console.log('fun')
}
console.log(callFn)
console.dir(callFn) //看見物件所有屬性內容  
```

純值 傳值(call by value) 
物件(陣列 函式)) 傳參考(call by reference)

# 深淺拷貝

```js
var family = {
    name: 'Hsu',
    member: {
        father: 'dad',
        monther: 'mom',
        other: 'someone'
    }
}
var newFamily = {}
for(var key in family) {
    console.log(key, family[key]);
    newFamily[key] =family[key];
}
newFamily.name = 'Chen'
console.log(family, newFamily)
newFamily.member.other = 'stranger'
console.log(family, newFamily) //for in只能做第一層的複製 第二層是傳參考的形式
//淺層複製  js for in, jQuery extend, ES6 assign


//jQuery
var newFamily2 = jQuery.extend({}, family);
//ES6
var newFamily3 = Object.assign({}, family)

//深層複製 deep copy 會將原本的物件轉成字串再轉回來 傳參考特性會沒有 
//console.log(family, JSON.stringify(family))
console.log(family, JSON.parse( JSON.stringify(family) )) 
var newFamily4 = JSON.parse( JSON.stringify(family) );
console.log(family === newFamily4)
newFamily4.name = 'Liao'
newFamily4.member.other = 'Deep'
console.log(family, newFamily4) //兩者完全無關  參考也都不一樣  
```

# 陣列

陣列是物件型別的一種  

```js
var newArray = [
    1,
    'Str',
    true,
    {
        name:'Jacob'
    }
];
console.log(newArray[3]); //[object Object] { name: "Jacob"}
console.log(newArray.3); //"error"
newArray.push(5);
newArray.name = 'Hsu'; //物件可隨意增加屬性 
newArray[5] ='Chen';
newArray[7] ='Liao'; //陣列6 empty 取值undefined
console.log(newArray); //name不屬於陣列裡面的長度

for(var i=0;i<newArray.length;i++) {
    console.log(newArray[i])
}
```

```js
var a = [1, 2, 3];
console.log(a, a[1], a.length)

//forEach 不是實體屬性 是陣列原型的屬性  
a.forEach(function(i){
    console.log(i)
});

(3) [1, 2, 3]
0: 1
1: 2
2: 3
length: 3  // length 也是一個物件的屬性  
__proto__: Array(0) //陣列的原型  可以透過點運算子不斷向上查找取得方法 例:forEach
    ...
    __proto__: Object //  陣列的原型 繼承物件的原型  所以陣列也可以使用物件原型的方法  例:toString   
```

```js
var a = [1, 2, 3];

var b = [4 ,5 ,6];
//新增方法到原型鏈上
a.__proto__.getLast = function() {
    return this[this.length-1]; //b[b.length-1]
}
console.log(a, b, a.getLast(), a.toString())
```

# JSON

[JSON - 維基百科](https://zh.wikipedia.org/wiki/JSON)  
儘管JSON是JavaScript的一個子集，但JSON是獨立於語言的文字格式  

JSON所有的屬性一定都是字串的形式  
物件可以用單引號`'` 但JSON一律用雙引號`"`  

SON 的格式是非常嚴格的，多一個逗號少一個逗號，都會導致出現錯誤，
所以最後一筆不可多了一個逗號

透過 `JSON.parse()` 出來的資料是一個物件，所以物件會有傳參考特性
後續的值變更，原本的值也會變更  

原生AJAX讀JSON
```js
//原生AJAX
function getData() {
    console.log(this.response)
    var data = JSON.parse(this.response);
    console.log(data);
}
var oReq = new XMLHttpRequest();
oReq.addEventListener("load", getData);
oReq.open("GET","family.json") //傳入的字串
oReq.send();
```
透過開發工具Network可以看結果  


# function 

在 JavaScript 中 function 是一個很特別的存在，它是可以當成物件來使用，
function 也是物件的一種，只是它是擁有程式區塊的能力物件而已
透過 「.」 即可做到新增屬性與值，所以function 在 JavaScript 是一個特殊的物件

```js
function statementFn() {
    console.log('函式陳述式', '具名函式');
    console.log(statementFn);
}
statementFn();

var expressionFn = function() {
    console.log('函式表達式','匿名函式'); //不是所有匿名函式 都是函式表達式
    console.log(expressionFn);
}
expressionFn()

var functionC = function functionD() {
    console.log(functionC, functionD)
    //具名函式能夠在函式內被調用
}
console.log(functionC)
console.log(functionC, functionD) //functoinD is not defind

var num = 1
var giveMeMoney = function giveMoreMoney(coin) {
    num += 1
    console.log('Exec giveMeMoney',num,coin)
    return coin>100 ? coin : giveMoreMoney(num * coin)
};
console.log(giveMeMoney(30)) //加錢到超過100元才停止
```

```JS
function callSomeFn(fn) {
    fn();
}
// 函數陳述式沒有名稱無法執行
// function (fn) {
//     fn();
// }
// 傳入的參數函式 如同函式表達式  不需要名稱
callSomeFn(function(){ console.log('執行函式') }) // 2定義一段函式並賦予到參數上
```

# 立即函式(IIFE)

[立即呼叫函式表達式](https://zh.wikipedia.org/wiki/立即调用函数表达式)（英文：immediately-invoked function expression，縮寫：IIFE）

```js
function fnA() {
    console.log('IIFE')
}
fnA();

// IIFE
(function IIFE() {
    console.log('立即函式', 'IIFE', '沒有fnA也可以執行','這裡是具名函式')
    // 1. 立即執行
    // 2. 無法再函式外被再次執行  
}());  //括號內層再補上小括號 

(function IIFE() {
})();  //小括號可以移到外層    
console.log(IIFE); //IIFE is not defined

(function() {
    console.log('立即函式', 'IIFE', '沒有fnA也可以執行')
    // 1. 立即執行
    // 2. 無法再函式外被再次執行  
}());


(function() {
    var name = 'Jacob';
    console.log(name)
    // 限制變數的作用域
})(); 


var whereParameter = (function(parameter) {
    console.log(parameter)
    return parameter;
})('參數在這'); 
console.log(whereParameter);

//記得養成好習慣 在立即函式前或後加分號

// 立即函式 傳遞變數
var a = {};
(function(b){
    b.person = 'jacob';
})(a)
;(function(c){
    console.log(c.person); //把另一個立即函式定義的變數印出來
})(a)

// 大型框架下 用全域物件傳值
(function(global){
    global.person = 'jacob';
})(window)
;(function(){
    console.log(person); //把另一個立即函式定義的變數印出來
})()

```

# 參數

```js
// callback function
function cbFn(name, a) {
    console.log(name+'你好'+a)
}
function funcB(fn) {
    fn('Jacob', 1) //實際執行在這
}
funcB(cbFn) //"Jacob你好1"
```

```js
function callArg(a) {
    console.log(a, arguments); //arguments 是一個類陣列 不是純陣列
    for(let index = 0; index < arguments.length; index++) {
        console.log(arguments[index]); // 1 2 3 '4' 
    }

    // 類陣列並沒有絕大多數陣列可使用的方法  
    // "TypeError: arguments.forEach is not a function
    arguments.forEach(function(){

    })
}
callArg(1, 2, 3, '4') //1, [object Arguments] { 0: 1, 1: 2, 2: 3, 3: "4"}
```

# 閉包 Closure

```js
function storeMoney() {
   var money = 1000;
   return function(price) {
      money = money + price
      return money
   }
}
//console.log( storeMoney()(100) ) // 1100
var mingMoney = storeMoney()
console.log(mingMoney) //function(price) {
console.log(mingMoney(100))
```


```js
function arrFunc() {
    var arr = [];
    for(var i=0;i<3;i++) {
        arr.push(function(){
            console.log(i);
        });
    }
    console.log('i', i) // 3 3 3 
    return arr;
} 
var fn = arrFunc();
fn[0]();
fn[1]();
fn[2]();
```

透過 立即函式  
```js 
function arrFunc() {
    var arr = [];
    for(var i=0;i<3;i++) {
        // 立即函式一個功能 限制作用域  
        (function(j){
            arr.push(function(){
                console.log(j);
            });
        })(i);
    }
    console.log('i', i) // 0 1 2 
    return arr;
} 
var fn = arrFunc();
fn[0]();
fn[1]();
fn[2]();
```

透過 let   
```js
function arrFunc() {
    var arr = [];
    for(let i=0;i<3;i++) {
        arr.push(function(){
            console.log(i); // 0 1 2 
        });
    }
    //console.log('i', i) // "error" let作用域只在for
    return arr;
} 
var fn = arrFunc();
fn[0]();
fn[1]();
fn[2]();
```

## 函式工廠  
給不同的值　做相同的事情
```js
function storeMoney(initVal) {
    var money = initVal || 1000
    return function(price) {
        money = money + price;
        return money;
    }
}
var MingMoney = storeMoney(100);
console.log(MingMoney(500)) // 600
```


```js
function storeMoney(initVal) {
    var money = initVal || 1000
    // 私有方法 可以做很多不同事情
    return {
        increase: function(price) {
            money += price
        },
        decrease: function(price) {
            money -= price
        },
        value: function() {
            return money;
        }
    }
}
var MingMoney = storeMoney(100);
MingMoney.increase(100);
MingMoney.increase(25);
MingMoney.decrease(25);
console.log(MingMoney.value()) // 200
```

## this

chrome / devTool / Sources / || 暫停按鈕 / 進入執行堆疊  

`this` 為關鍵字 在每個執行環境存在  

this 的調用方式
作為物件方法  關注在哪個物件下呼叫  `Object.fn()` this 指向 Object
簡易呼叫  (不建議調用this)
bind, apply, call 方法  
new  
DOM事件處理器  
箭頭函式(ES6)  

### simple call 簡易呼叫 

```js
var myName = 'Jacob';
function callName() {
    console.log(this, this.myName)
}
callName() // this -> window
// 盡可能不要使用simple call的this
```

```js
(function(){
    console.log(this.myName);
    function callFn() {
        console.log(this.myName);
    }
    callFn(); //simple call 看到函式是直接執行的 就是簡易呼叫 執行閉包內函式也是
})();
```

```js
// callback
function myCb(callback) {
    var money = 100
    return callback(money)
}
myCb(function(money) {
   console.log(this.myName, money+100)
})
```

```js
var a = [1, 2, 3]
// forEach 後方是插入一個callback函式
a.forEach(function(i){
    console.log(this.myName, i);
})

var family = {
    myName: 'Hsu',
    callName: function() {
        // var self = this; // vm , that 
        setTimeout(function(){
            console.log(this.myName) // simple call this->window 'Jacob' 無法取得物件的myName 'Hsu'
            console.log(self.myName) // 物件的myName 'Hsu'
        }, 1000)
    }
    family.callName();
}
```

### Call, appply, bind

```js
var team = {
    myName: 'Jacob'
}
function fn(para1, para2) {
    console.log(this, para1, para2)
}
fn(1, 2); //simple call
fn.call(team, 1, 2); // call 是立刻執行
fn.apply(team, [3,4]); // apply 是立刻執行  差別在以陣列方式呈現

var fn2 = fn.bind(team, 5, 6); // bind 非立刻執行  
fn2(6); // [object Object] 5 6 順序執行參數所以是6  
fn2(1, 2); // [object Object] 5 1 順序執行參數所以是1  
```

```js
function fn(para1, para2) {
    console.log(this, para1, para2)
}
// 進階概念
fn.call(1, 'Jacob', 'Jessica') //傳純值 Number{1} 'Jacob', 'Jessica' 已建構式方式呈現 物件的型別

fn.call('Str', 'Jacob', 'Jessica')
fn.call(undefined, 'Jacob', 'Jessica') // null 、undefined 將會被置換成全域變數 [object Window] 'Jacob', 'Jessica'
```

[MDN call()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call)  


### 嚴格模式

```js
(function(){
    'use strict';
    name = 'Jacob';  // "error" name is not defined
})()
```

```js
function fn(para1, para2) {
    'use strict'; // 有加入嚴格模式 this所指向的window會變undefined
    console.log(this, para1, para2) // 1 "Jacob" "Jessica"  嚴格模式下 純值維持原型別 不以建構式方式呈現
}
fn.call(1, 'Jacob', 'Jessica') 
fn.call(undefined, 'Jacob', 'Jessica') // undefined "Jacob" "Jessica"
// 簡易呼叫下 盡可能不要調用this 因為它本質就是undefined
```

### this: DOM

```html
<button onclick="console.log(this)">this is btn</button>
<button onclick="console.dir(this)">this is btn</button>
```

[console.dir(object)](https://developer.mozilla.org/zh-CN/docs/Web/API/Console/dir)  

# new

```js
function Dog(name, color, size) {
    this.name = name;
    this.color = color;
    this.size = size;
}
var Bibi = new Dog('比比', '棕色', '小')
console.log(Bibi)  

//函式本身就是一個物件 函式物件有一個特別的屬性 prototype  
//透過prototype所新增的屬性 就會做原型上的方法  函式物件特有的屬性
Dog.prototype.bark = function () {
    console.log(this.name, 'barking')
}
// __proto__ 物件上  
// prototype 函式上  
// 調整原型的方法時 最好的方式是從函式本身的原型屬性上去調整
console.log(Dog.prototype === Bibi.__proto__) // true  
```

```js
var b = new String('bcde');
console.log(b)
console.dir(String)
String.prototype.lastText = function() {
    return this[this.length - 1];
}
console.log(b.lastText());

Number.prototype.secondPower = function() {
    return this * this;
}
var num = 5;
console.log(num.secondPower());

var date = new Date();
console.log(date);
console.dir(Date);
Date.prototype.getFullDate = function() {
    var dd = String(this.getDate());
    var mm = String(this.getMonth()+1);
    var yyyy = this.getFullYear();

    var today = yyyy + '/' + mm + '/' +dd;
    return today;
}
console.log(date.getFullDate());
```

## 繼承

[Object.create()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
```js
var a = []
//Object > Array > a (實體)

//原型鏈上新增一個層級  
//Object > Animal > Dog > 實體
//Object > Animal > Cat > 實體

// Object.create() 可以把其他物件作為原型使用

var dog = {
    name: '狗',
    bark: function() {
        console.log(this.name + ' barking')
    }
} 
var Corgi = Object.create(dog); //Corgi 把 dog 作為原型使用  
Corgi.name = 'Welsh Corgi' 
console.log(Corgi)
```

```js
function Animal(family) {
    this.kingdom = '動物界'
    this.family = family || '貓科'
}
Animal.prototype.move = function() {
    console.log(this.name + ' can move') 
}
function Dog(name, size) {
    Animal.call(this, '犬科')
    this.name = name;
    this.size = size || 'small'
}
Dog.prototype = Object.create(Animal.prototype)
Dog.prototype.constructor = Dog; // 狗的原型原本直接繼承於動物界的原型 constructor 會被覆蓋所以補回原本建構函式
Dog.prototype.bark = function() {
    console.log(this.name + ' barking')
}

var Chihuahua = new Dog('Chihuahua','small');
console.log(Chihuahua)  
Chihuahua.bark();
Chihuahua.move();
Chihuahua.family // undefined  目前只有繼承原型prototype 但無繼承動物界的建構函式 Animal.call
```

如果瀏覽器不支援 `Object.create()`
這時候我們會寫一些程式來填補某些瀏覽器不支援的情況，我們把這些程式稱做 `polyfill`

## 屬性特徵

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
}
console.log(obj)
//Object.defineProperty()
// 屬性，調整屬性的特徵
// 1. 值  2. 可否寫入 3. 可否被刪除  4. 可否被列舉
//Object.defineProperty(物件, 屬性, 參數)

// being explicit
Object.defineProperty(obj, 'a', {
  enumerable: true,
  configurable: true,
  writable: false,
  value: 4
});
console.log(obj)

// "TypeError: Cannot assign to read only property 'a' of object '#<Object>'
(function() {
    'use strict';
    obj.a = 5;
}())
```

[Object.defineProperty()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 