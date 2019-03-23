title: RESTful API
---

RESTful 是目前最流行的 API 設計規範，用於 Web 數據接口的設計。

## 動詞

動詞通常就是五種 HTTP 方法，對應 CRUD 操作。

>POST：新建（Create）  
GET：讀取（Read）  
PUT：更新（Update）   
PATCH：更新（Update），通常是部分更新      
DELETE：刪除（Delete）

### 動詞 + 賓語

RESTful 的核心思想就是，客戶端發出的數據操作指令都是"動詞 + 賓語"的結構。
比如，`GET /articles`這個命令，`GET`是動詞，`/articles`是賓語。

### 使用複數 URL

建議都使用複數 URL，比如`GET /articles/2`要好於`GET /article/2`。 

### 避免多級 URL

資源需要多級分類，因此很容易寫出多級的 URL，比如獲取某個作者的某一類文章。
> GET /authors/12/categories/2

這種 URL 不利於擴展，語義也不明確
更好的做法是，除了第一級，其他級別都用查詢字符串表達。
> GET /authors/12?categories=2

## 狀態碼

>1xx：相關信息  
2xx：操作成功  
3xx：重定向  
4xx：客戶端錯誤  
5xx：服務器錯誤  

API 用不到301狀態碼（永久重定向）和302狀態碼（暫時重定向，307也是這個含義），因為它們可以由應用級別返回，瀏覽器會直接跳轉，API 級別可以不考慮這兩種情況。

API 用到的3xx狀態碼，主要是`303 See Other`，表示參考另一個 URL。它與302和307的含義一樣，也是"暫時重定向"，區別在於302和307用於GET請求，而303用於POST、PUT和DELETE請求。收到303以後，瀏覽器不會自動跳轉，而會讓用戶自己決定下一步怎麼辦。
下面是一個例子。  

```js
HTTP/1.1 303 See Other
Location: /api/orders/12345
```

### HATEOAS 提供鏈接

API 的使用者未必知道，URL 是怎麼設計的。
一個解決方法就是，在回應中，給出相關鏈接，便於下一步操作。這樣的話，用戶只要記住一個 URL，就可以發現其他的 URL。這種方法叫做 HATEOAS。

例 GitHub 的 API 都在 [api.github.com](https://api.github.com/) 這個域名下可查找

## References

https://blog.florimondmanca.com/restful-api-design-13-best-practices-to-make-your-users-happy  
http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html