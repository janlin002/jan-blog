# with

> 沒事不要用 `with`

## 什麼是 `with`? 怎麼用？

with的初衷是为了避免冗余的对象调用：

```js
foo.bar.baz.x = 1;
foo.bar.baz.y = 2;
foo.bar.baz.z = 3;

// 使用 with 改寫
with(foo.bar.baz){
    x = 1;
    y = 2;
    z = 3;
}
```

不過其實用基本的 JavsScript 就能達到一樣的效果了

```js
const a = foo.bar.baz

a.x = 1
a.y = 2
a.z = 3
```


### 為什麼不要用 `with`?

1. 性能
2. 不可预测
3. 优化

#### 參考文章

[深入JavaScript with语句](https://swordair.com/javascript-with-statement-in-depth/)
