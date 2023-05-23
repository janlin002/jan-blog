# 型別防衛 (Type Guard)

在 TypeScript 裡，我們時常遇到需要對 union type （例如：A | B）裡面的其中一個 type 才有的屬性做操作，這時執行檢查讓型別能被限縮的技巧就是 Type Guard。

有幾種方式可以實現 Type Guard:

1. typeof type guard

```js
function isString(value: string | undefined): string {
    if(typeof === 'string'){
        return string
    }
}
```

我們只要把typeof type guard 放在 if 條件句中，就可以做到 Type Guard 

2. type predicates (型別謂語)

寫法是:

```
parameterName is Type
```

`parameterName` 必須要是函式中參數的名稱

```js
let value: string | undefined;

function isString(value): value is string {
  return typeof value === 'string';
}
```

參考文章:

[Day18: 【TypeScript 學起來】Narrowing Part 2](https://ithelp.ithome.com.tw/m/articles/10277022)

[[擊敗前端面試大作戰] Typescript narrowing and Type guard](https://ithelp.ithome.com.tw/articles/10303220)

[TypeScript：Type Guard 的小細節](https://chentsulin.medium.com/typescript-type-guide-%E7%9A%84%E5%B0%8F%E7%B4%B0%E7%AF%80-9b1f2874dbad)