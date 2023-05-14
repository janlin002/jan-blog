# Reference Vs Value In JavaScript

<iframe width="100%" height="500" src="https://www.youtube.com/embed/-hBJz2PPIVE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

這部影片是在講解 JS 中的 by value 跟 by reference

object 型別的才會有 by reference 的問題

如果是直接對複製過來的值，做修改就會更改到原本的部分

```js
const a = [1,2]
b = a

b.push(3)

// a => [1,2,3]
// b => [1,2,3]
```

不過如果是全部置換的話，就不會有個問題，因為等同於記憶位置修改了

```js
const a = [1,2]
b = a
b = [2,1]

// a => [1,2]
// b => [2,1]
```


### 補充文章

[[JavaScript] Javascript中的傳值 by value 與傳址 by reference](https://medium.com/itsems-frontend/javascript-pass-by-value-reference-sharing-5d6095ae030b)