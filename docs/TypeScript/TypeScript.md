# TypeScript 學習筆記

### 為什麼需要 TypeScript？

因為 JavsScript 是弱型別的語言，也因為這樣型別可以換來換去，增加了發生錯誤的機率，TypeScript 就是為了解決這樣的問題，透過 TypeScript 我們需要嚴格定義型別的部分，減少出錯的機會

### 聯集 (Union)

讓我們可以不侷限於一個特定型別

```js
let age: number | string
```