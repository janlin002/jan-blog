# Tuple 元組

Tuple並不是JavaScript原生的概念，是TypeScript提供的一種資料結構

Tuple可以想成是一個嚴格的陣列，陣列的元素是固定數量的，且每個元素的型別都是已知的，但型別不用相同。

```js
let person: [string, number];

person = ["John", 18]

//[string, number]這就是元組的樣子，你可以決定他要多長（有幾個值），但長度得固定。
```
或是我們可以幫元組加上label，提升代碼的可讀性

```js
let person: [name: string, age: number];

person = ["John",18]

let person :(string | number)[]=['Una','Lin',18]
```