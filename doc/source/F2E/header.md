title: Header
---

[HTTP Referer 教程](http://www.ruanyifeng.com/blog/2019/06/http-referer.html)  

`Referer` 提供訪問來源的信息。 **引薦人（referrer）**，誰引薦了你？
HTTP 協議在請求（request）的頭信息裡面，設計了一個Referer字段，給出 **"引薦網頁"** 的 URL。  字段是可選的。 

主要是以下三種場景，會發送Referer字段。 
 
（1）用戶點擊網頁上的鏈接。  
（2）用戶發送表單。  
（3）網頁加載靜態資源，比如加載圖片、腳本、樣式。  

###　Referer 的作用

涉及隱私，很多時候不適合發送`Referer`字段

不適合暴露 URL。一是功能URL，即有的URL不要登錄，可以訪問，就能直接完成*密碼重置、郵件退訂*等功能。

還有一種特殊情況，需要定製Referer字段。比如*社交網站*上，用戶在對話中提到某個網址。這時，不希望暴露用戶所在的原始網址，但是可以暴露社交網站的域名，讓對方知道，是我貢獻了你的流量。



[nginx 真實IP Remote-Addr X-Forwarded-For X-Real-IP](https://www.twblogs.net/a/5c17b0adbd9eee5e4184514e)  

[`X-Forwarded-For（XFF）`](https://zh.wikipedia.org/wiki/X-Forwarded-For)是用來辨識通過HTTP代理或負載均衡方式連接到Web伺服器的用戶端最原始的IP位址的HTTP請求頭欄位。