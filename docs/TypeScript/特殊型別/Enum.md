# Enum 列舉

枚舉跟元組一樣，都不是Js原生的部分，透過列舉我們可以輕鬆的定義一系列邏輯相同的常數值

(Enum 可以想成就是將東西一個一個列出來，通常會用它來管理多個同系列的常數)

寫法:

透過 `enum` 去宣告一個新的枚舉
```js
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}
```

我們將 Direction 的 Up，設為1，那麼由於枚舉的特性，他會自動幫我們定義好下面的 `Down` `Left` `Right`

寫法就如同:

```js
enum Direction {
  Up = 1,
  Down = 2,
  Left = 3,
  Right =4
}
```

分三種型別，分別為數字列舉(Number enum)、字串列舉(String enum)和異構列舉(Heterogeneous enum)

參考文章:

[【Day 12】TypeScript 資料型別 - 元組(Tuple) & 列舉(Enum)](https://ithelp.ithome.com.tw/articles/10221546)