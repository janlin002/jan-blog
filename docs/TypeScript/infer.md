# infer

在 TS 中我們常會使用 `Conditional Types`去做判斷

```ts
T extends U ? X : Y
```

這樣寫代表的是: 當 `T` 能指派給 `U`，則該型別為 `X`，反之則型別為 `Y`。

不過當判斷一多時，就會變得很混亂

```ts
type TypeName<T> = T extends string
  ? "string"
  : T extends number
  ? "number"
  : T extends boolean
  ? "boolean"
  : T extends undefined
  ? "undefined"
  : T extends Function
  ? "function"
  : "object";
```

當我們希望條件符合特定的型別結構，但某個型別希望交由 TypeScript 推斷時，可以加入 infer 關鍵字來幫忙。

infer 關鍵字必須使用在「條件類型的子句」，也就是 extends 後面、? 前面的位置。

```ts
type Item<T> = T extends (infer U)[] ? U : never;
```

等同於:

```ts
Item<string[]> // string
Item<number[]> // number
```

### 參考文章

[TypeScript：infer 的強大功用](https://chentsulin.medium.com/typescript-infer-%E7%9A%84%E5%BC%B7%E5%A4%A7%E5%8A%9F%E7%94%A8-9b43c4eac6fb)
