# 型別斷言 (Type Assertion)

类型断言（Type Assertion）可以用来手动指定一个值的类型。

Assertion 可以讓 TypeScript 允許你覆盖它的推断的型別。

寫法是:

```js
值 as 类型

// 或是

<类型>值
```

当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型中共有的属性或方法，但有时候，我们确实需要在`还不确定类型的时候就访问其中一个类型特有的属性或方法`

```js
interface Cat {
  name: string;
  run(): void;
}
interface Fish {
  name: string;
  swim(): void;
}

function isFish(animal: Cat | Fish) {
  if (typeof animal.swim === "function") {
    return true;
  }
  return false;
}
```

上面的例子中，获取 animal.swim 的时候会报错。

此时可以使用类型断言，将 animal 断言成 Fish：

```js
interface Cat {
    name: string;
    run(): void;
}
interface Fish {
    name: string;
    swim(): void;
}

function isFish(animal: Cat | Fish) {
    if (typeof (animal as Fish).swim === 'function') {
        return true;
    }
    return false;
}
```

需要注意的是，`类型断言只能够「欺骗」TypeScript 编译器，无法避免运行时的错误`，反而滥用类型断言可能会导致运行时错误

```js
interface Cat {
    name: string;
    run(): void;
}
interface Fish {
    name: string;
    swim(): void;
}

function swim(animal: Cat | Fish) {
    (animal as Fish).swim();
}

const tom: Cat = {
    name: 'Tom',
    run() { console.log('run') }
};
swim(tom);
```

上面的例子编译时不会报错，但在运行时会报错

```js
Uncaught TypeError: animal.swim is not a function`
```

參考文章:

[typescript-tutorial](https://github.com/xcatliu/typescript-tutorial/blob/master/basics/type-assertion.md)

[型別介紹 part3 - 型別斷言](https://ithelp.ithome.com.tw/articles/10295260)

[Day05:【TypeScript 學起來】TS 指定型別的三種方法](https://ithelp.ithome.com.tw/articles/10263795)
