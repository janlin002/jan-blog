# typeof

JavaScript 的開發者都知道，在 JS 中有 typeof operator 可以使用，主要功能是在幫我們判斷型別

不過在 TypeScript 中的 typeof 卻不一樣

```js
typeof = Typeof Type Operator
```

我們都知道在開發 TS 時，如果對於型別不確定，可以將滑鼠滑到變數上面，他會顯示 TS 所判定的型別，不過自動推導出來的型別需要滑鼠移上去時才看得到，有沒有什麼方式能夠把這個「自動推導的結果」建立成一個可以被使用的型別呢？

typeof 就是在做這件事

```ts
const conference: {
  name: string;
  year: number;
  isAddToCalendar: boolean;
  website: string;
};

type Conference = typeof conference;
```

### 參考文章

[[Day13] TS：什麼！這個 typeof 和我想的不一樣？](https://pjchender.dev/ironman-2021/ironman-2021-day13/)