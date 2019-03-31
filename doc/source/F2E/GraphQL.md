title: GraphQL
---

GraphQL 是一個用於 API 的查詢語言，是一個使用基於類型系統來執行查詢的服務端運行時（類型系統由你的數據定義）。GraphQL 並沒有和任何特定數據庫或者存儲引擎綁定，而是依靠你現有的代碼和數據支撐。


![GraphQL](https://i.imgur.com/Jdvb0fV.png)  


使用一個 API 系統就像在百貨公司的地下美食廣場買晚餐，
傳統的 `RESTful API` 會要求你要一家一家 (很多 route) 去點餐，耗時又費力。

`GraphQL` 的體驗就如同使用APP一樣，百貨公司的餐飲店家們開發出一款點餐APP整合各家的點餐介面，消費者只要把想點的各家食物放進菜單，一鍵送出後就只要等待所有餐點送來桌上，省時又不費力！此外通過 APP 還可以更容易取得額外資訊如餐廳的聯絡方式





> 有了 GraphQL ，你可以把你的商業模型 (business model) 像圖形 (graph) 一樣串連起來 
不同或相同type 的資料可以串接再一起，使得 GraphQL 只要一筆 query 就能一次拿全資料且資料格式非常有彈性！
反觀 RESTful API 同樣的資料需要多筆 request 才能拿到且格式難以調整。

| 優點  | 缺點  |  
|---|---|
| 資料只拿剛好且彈性十足  | 過於自由、規範少  |   
| 程式即文檔  | 學習成本  | 
| 前端控制權提升  | 相關社群仍在開發中 (Apollo)  |   
| 強型別  | Server Side Caching 實作困難  |  


Server Side Caching 實作困難
> RESTful API 的 endpoint 固定且資料需求單純，然而 GraphQL 難以保證每次 request 的模樣，因此較難實作 Caching



# References

https://graphql.cn/learn/  
https://ithelp.ithome.com.tw/articles/10200678  