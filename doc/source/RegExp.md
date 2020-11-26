title: 正規表達式 regexp
---

[正規表達式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Regular_Expressions)  
[2019年JS正则大全(常用)](https://juejin.im/post/5d245d4151882555300feb77?utm_source=gold_browser_extension)  




[js正则表达式，限1-2位整数，或者至多含有两位小数](https://blog.csdn.net/bestcxx/article/details/60772406)

```js
//1、只能输入数字或者小数点    仅整数,整数加小数
var reg1=/(^[0-9]{1,2}$)|(^[0-9]{1,2}[\.]{1}[0-9]{1,2}$)/;
```

password

限制密碼必須是八個字符，包括一個大寫字母，一個特殊字符和字母數字字符

至少八個字符，至少一個字母和一個數字：  
`^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$`
最少八個字符，至少一個大寫字母，一個小寫字母和一個數字：  
`^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$`
至少八個字符，至少一個大寫字母，一個小寫字母，一個數字和一個特殊字符：  
`^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*?&])[A-Za-z\d$@$!%*?&]{8,}`
最少八個最多十個字符，至少一個大寫字母，一個小寫字母，一個數字和一個特殊字符：  
`^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*?&])[A-Za-z\d$@$!%*?&]{8,10}`

```js
export const isValidPWD = (pwd: string) => {
  const reg = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[A-Za-z\d]{8,}/
  return reg.test(pwd)
}
```


email

```js
var firstRegExp = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
console.log(firstRegExp.test('jacob.hsu.tw@gmail.com')); //true
console.log(firstRegExp.test('jacob.hsu.tw')); //false
```

|規表示式的特定字元	|說明	|等效的正規表示式
|---|---|---|---|---|
|\d	|數字	|[0-9]
|\D	|非數字	|[^0-9]
|\w	|數字、字母、底線	|[a-zA-Z0-9_]
|\W	|非 \w	|[^a-zA-Z0-9_]
|\s	|空白字元	|[ \r\t\n\f]
|\S	|非空白字元	|[^ \r\t\n\f]
|[xyz]	|比對中括弧內的任一個字元	|/[ecm]/ 可比對 “welcome” 中的 “e” 或 “c” 或 “m”
|[^xyz]	|比對不在中括弧內出現的任一個字元	|/[^ecm]/ 可比對 “welcome” 中的 “w”、”l”、”o”，可見出其與 [xyz] 功能相反。（同時請注意 /^/ 與 [^] 之間功能的不同。）

## match

[String.prototype.match()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String/match)

```js
const pa = '賓夕法尼亞州是美國的州份之一，正式名稱為「賓夕法尼亞邦」(Commonwealth of Pennsylvania)';
const pa_us = pa.match( /\((.+?)\)/g ) // ["(Commonwealth of Pennsylvania)"]
const res = pa_us[0].replace(')', '').substring(1);
console.log(res) // "Commonwealth of Pennsylvania"
```
