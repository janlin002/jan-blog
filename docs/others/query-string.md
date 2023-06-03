#  Query String

## 什麼是 Query String？

query string 是使用者傳遞請求的方法之一，讓我們可以輕鬆的**利用網址傳遞一些隱藏資訊做紀錄**

所謂的query string就是請求url之中 `?` 後面的參數，例如下面例子中的 `lastname` 和 `firstname`

```
https://www.develop-note.com/api/custom?lastname=chang&firstname=kirai
```

## Query String 相關套件

雖然我們可以透過 `window.location.search` 取得 `query string`，然後透過 `正則` 或是 `String.split` 等方法取得詳細資料，不過這樣太麻煩了，所以以下推薦兩款常用的套件

[query-string](https://github.com/sindresorhus/query-string)

[qs](https://github.com/ljharb/qs)

### stringify

在這兩個套件中，都有一個 `stringify()` 方法可以組成 `query string` 的格式

![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*U8UB_lmyQGelfQRpha_PBw.png)

圖片取自: [你所不知道的 query string 小細節](https://medium.com/starbugs/%E4%BD%A0%E6%89%80%E4%B8%8D%E7%9F%A5%E9%81%93%E7%9A%84-query-string-%E5%B0%8F%E7%B4%B0%E7%AF%80-56498dc0645)

### parse

parse 基本上就是 stringify 的相反，將 query string 轉成物件方便開發者對其進行操作

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*6ZHU9f4DFyKi3MObQ01r9A.png)

圖片取自: [你所不知道的 query string 小細節](https://medium.com/starbugs/%E4%BD%A0%E6%89%80%E4%B8%8D%E7%9F%A5%E9%81%93%E7%9A%84-query-string-%E5%B0%8F%E7%B4%B0%E7%AF%80-56498dc0645)

### 參考文章

[React 中優雅使用網址參數 Query String](https://medium.com/itsoktomakemistakes/react-%E4%B8%AD%E5%84%AA%E9%9B%85%E4%BD%BF%E7%94%A8%E7%B6%B2%E5%9D%80%E5%8F%83%E6%95%B8-query-string-540bacd08486)

[iris的 query string](https://ithelp.ithome.com.tw/articles/10250651)

[你所不知道的 query string 小細節](https://medium.com/starbugs/%E4%BD%A0%E6%89%80%E4%B8%8D%E7%9F%A5%E9%81%93%E7%9A%84-query-string-%E5%B0%8F%E7%B4%B0%E7%AF%80-56498dc0645)