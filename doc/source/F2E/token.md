title: Token
---

[JSON Web Token 入門教程](http://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)  
`JSON Web Token`（縮寫 `JWT`）是目前最流行的跨域認證解決方案 

A 網站和 B 網站是同一家公司的關聯服務。現在要求，用戶只要在其中一個網站登錄，再訪問另一個網站就會自動登錄，請問怎麼實現？  

> 一種方案是服務器索性不保存 session 數據了，所有數據都保存在客戶端，每次請求都發回服務器。`JWT` 就是這種方案的一個代表。