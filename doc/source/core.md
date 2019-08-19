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