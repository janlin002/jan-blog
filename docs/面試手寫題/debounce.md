# debounce 防抖

## 什麼是 debounce ？

防抖 (debounce) 函式是指，將多次操作優化為，只在最後一次執行。又可以說是讓使用者在觸發相同事件（如卷軸或是輸入）的情境下，停止觸發綁定事件的效果，直到使用者停止觸發相同事件。

現實中的例子: 就是排隊搭公車的時候，司機在開門後，會待每一個乘客都上車後，最後才會關上門。

## 實作 debounce

```js
function debounce(fn, delay = 500) {
  let timer;

  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn(...args);
    }, delay);
  };
}
```

## 參考資料
[Debounce & Throttle — 那些前端開發應該要知道的小事(一)](https://medium.com/@alexian853/debounce-throttle-%E9%82%A3%E4%BA%9B%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC%E6%87%89%E8%A9%B2%E8%A6%81%E7%9F%A5%E9%81%93%E7%9A%84%E5%B0%8F%E4%BA%8B-%E4%B8%80-76a73a8cbc39)

[手寫防抖 (debounce) 函式](https://www.explainthis.io/zh-hant/interview-guides/javascript-whiteboard/debounce)

[手寫節流 (throttle) 函式](https://www.explainthis.io/zh-hant/interview-guides/javascript-whiteboard/throttle)
