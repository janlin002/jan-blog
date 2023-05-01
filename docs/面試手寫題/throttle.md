# throttle

## 什麼是 throttle ？

節流 (throttle) 指的是，在一段時間內只會執行一次觸發事件的回調 (callback) 函式，若在這之中又有新事件觸發，則不重新執行。

實際中的例子：滾動事件

## 實作 throttle

```js
function throttle(fn, delay = 500) {
  let timer = null;

  return (...args) => {
    // 如果有計時器，表示還在 delay 的秒數內
    // 直接 return，不往下執行程式碼
    if (timer) return;

    timer = setTimeout(() => {
      fn(...args);
      timer = null;
    }, delay);
  };
}
```
## 參考資料

[手寫節流 (throttle) 函式](https://www.explainthis.io/zh-hant/interview-guides/javascript-whiteboard/throttle)