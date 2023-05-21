# React with TypeScript

[教學連結](https://www.totaltypescript.com/tutorials/react-with-typescript)

## Introduction

### Adding React to a TypeScript Project

剛開始我們創建 React TypeScript 專案時，可能會遇到以下幾點問題

![not-install-types](../../static/img/not%20install%20types.png)

會報錯的原因是因為我們沒有下載 types

> types: 

解決方法就是:

```
npm i --save-dev @types/react
```

再來 dev 的部分報錯是因為我們目前使用的是 `tsx` 寫法，所以將副檔名由 `.ts` 改成 `.tsx` 即可

不過將副檔名更改過後卻有新的問題

![still-not-working](../../static/img/change%20to%20tsx%20still%20not%20working.png)

會報這個錯是因為編輯器認為: 「除非提供“--jsx”標誌，否則不能使用 JSX」，這個問題要解決的話，我們需要到 TS 的設定檔中做一些更改

```js
{
  "compilerOptions": {
    ...
    "jsx: "preserve"
```

這樣就可以正常運行了

### TypeScript in React Frameworks

...略

### Navigating JSX Types

...略

## Components

### 

## Hooks