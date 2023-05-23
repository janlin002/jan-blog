# 函式重載 (funciton overload)

函數重載（Function Overloading）是一種程式設計技術，它允許開發者在定義函數時，指定不同的參數型別，以及不同的回傳型別。

當我們在 TS 中使用 Unions 時，函式變得很複雜，並且我們會多做很多的判斷

```js
type Combinable = string | number

function add(a: Combinable, b: Combinable): Combinable{
  if(typeof a === 'string' || typeof b === 'string'){
    return a.toString() + b.toString()
  }
  return a + b
}
const result = add(1, 5)
```

這時候會報錯，因為typeScript認為Combinable不具備toString方法，這時候有兩種方式可以解決

1. 型別斷言

這樣可以明確的跟 TS 說，我這邊是要使用 `number`
```js
const result = add(1, 5) as number
```
2. Function Overloads

在 funciton 前面直接對他的型別做定義
```js
function add(a: number, b: number): number
function add(a: string, b: string): string
```


參考文章:

[學習TypeScript中的函數重載：深入了解函數的功能與應用](https://badgameshow.com/steven/typescript/%E5%AD%B8%E7%BF%92typescript%E4%B8%AD%E7%9A%84%E5%87%BD%E6%95%B8%E9%87%8D%E8%BC%89%EF%BC%9A%E6%B7%B1%E5%85%A5%E4%BA%86%E8%A7%A3%E5%87%BD%E6%95%B8%E7%9A%84%E5%8A%9F%E8%83%BD%E8%88%87%E6%87%89%E7%94%A8/)

[TypeScript — Advance Types(上)](https://medium.com/summers-life/typescript-advance-types-9e569b4f6ff2)

[TypeScript — Advance Types(下)](https://medium.com/summers-life/typescript-advance-types-%E4%B8%8B-70a802ceac92)
