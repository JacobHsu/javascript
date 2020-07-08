# [if...else](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/if...else)

## 條件組合的問題

規則是： 
1.在預熱中參與活動，vip用戶贈送 1000 積分，普通用戶贈送 700 積分。 
2.在進行中參與活動，vip用戶贈送 800 積分，普通用戶贈送 300 積分。 

```js
let status=1
let type=2
if(status===1){
     if(type===1){
           console.log('普通用戶在預售中參與活動，贈送700積分')
    }
    else if(type===2){
           console.log('vip用戶在預售中參與活動，贈送1000積分')
    }
}
else if(status===2){
     if(type===1){
           console.log('普通用戶在進行中參與活動，贈送300積分')
    }
    else if(type===2){
           console.log('vip用戶在進行中參與活動，贈送800積分')
    }
}
```

可以使用 `obj`寫法，如果以後有什麼條件改了，直接改 obj 這個配置就好

```js
let obj={
   'status=1&type=1':'普通用戶在預售中參與活動，贈送700積分',
   'status=1&type=2':'vip用戶在預售中參與活動，贈送1000積分',
   'status=2&type=1':'普通用戶在進行中參與活動，贈送300積分',
   'status=2&type=2':'普通用戶在進行中參與活動，贈送800積分'
}

console.log(obj[`status=${status}&type=${type}`])
```

[特定场景下代替优化 if-else 的方案](https://juejin.im/post/5efc55496fb9a07e9a079a5e?utm_source=gold_browser_extension)