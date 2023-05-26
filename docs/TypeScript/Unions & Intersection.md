# Unions(聯合型別) and Intersection(交集型別) Types

## Unions(聯合型別)

聯合型別（Union Types）表示取值可以為多種型別中的其中一種。跟 JavaScript `||` 的概念是一樣的。

```ts
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
printId(101); //ok
printId("202"); //ok
```

### 存取聯合型別的屬性或方法

當 TypeScript 不確定一個聯合型別的變數到底是哪個型別的時候，我們只能存取此聯合型別的所有型別裡共有的屬性或方法。

```ts
function printId(id: number | string) {
  console.log(id.toString());
}
```

> 對於使用 `Unions` 的變數做操作時，請特別注意該 `methods` 必須是兩種型別都通用，不然就需要使用 `typeof` 去解決

```ts
function printId(id: number | string) {
  console.log(id.toUpperCase());
}

//error: Property 'toUpperCase' does not exist on type 'string | number'.
//Property 'toUpperCase' does not exist on type 'number'.
```

## Intersection(交集型別)

交集型別(Intersection Type) 跟 JavaScript 的 `&&` 概念相同， 使用 `&` 表示其定義的值都必須同時符合兩種型別。

```ts
function printId(id: number & string) {
  console.log("Your ID is: " + id);
}
printId(101); //error
printId("202"); //error
```

這邊 TS 會報錯，原因是因為 `id` 不可能同時符合型別為 `number` 跟 `string`，所以會被判定型別為 `never`

```ts
interface Colorful {
  color: string;
}

interface Circle {
  radius: number;
}

//用type aliases 宣告 ColorfulCircle 型別，需滿足 Colorful 及 Circle 型別
type ColorfulCircle = Colorful & Circle;

//帶入的參數需滿足 ColorfulCircle 型別
function draw(circle: ColorfulCircle) {
  console.log(`Color was ${circle.color}`);
  console.log(`Radius was ${circle.radius}`);
}

draw({ color: "blue", radius: 42 }); // ok
draw({ color: "red", raidus: 42 }); //error
```

### 參考文章

[Day11:【TypeScript 學起來】只有 TS 才有的型別 : Union Types(聯合型別) / Intersection types (交集型別)](https://ithelp.ithome.com.tw/articles/10271768)

[[TS] Unions and Intersection Types](https://pjchender.dev/typescript/ts-unions-intersections/)
