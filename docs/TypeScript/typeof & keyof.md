# typeof & keyof

## typeof

JavaScript 的開發者都知道，在 JS 中有 typeof operator 可以使用，主要功能是在幫我們判斷型別

不過在 TypeScript 中的 typeof 卻不一樣

```js
typeof = Typeof Type Operator
```

我們都知道在開發 TS 時，如果對於型別不確定，可以將滑鼠滑到變數上面，他會顯示 TS 所判定的型別，不過自動推導出來的型別需要滑鼠移上去時才看得到，有沒有什麼方式能夠把這個「自動推導的結果」建立成一個可以被使用的型別呢？

typeof 就是在做這件事

```ts
const conference: {
  name: string;
  year: number;
  isAddToCalendar: boolean;
  website: string;
};

type Conference = typeof conference;
```

這樣 Conference 就擁有跟 conference 一樣的型別

## keyof

keyof 顧名思義就是把「物件型別（object type）」的 key 拿出來，但要留意的是，這裡提到的「物件型別」是指 TypeScript 的型別不是指 JavaScript 的物件

在了解 keyof 之前，我們必須先了解 字面量类型(literal types)

### 字面量类型(literal types)

字面量是 JavaScript 本身提供的一个准确变量

在这里，我们创建了一个被称为 foo 变量，它仅接收一个字面量值为 Hello 的变量：

```ts
let foo: 'Hello';
foo = 'Bar'; // Error: 'bar' 不能赋值给类型 'Hello'
```

他不能做二次的賦值

它们本身并不是很实用，但是可以在一个联合类型中组合创建一个强大的（实用的）抽象

```ts
type CardinalDirection = 'North' | 'East' | 'South' | 'West';

function move(distance: number, direction: CardinalDirection) {
  // ...
}

move(1, 'North'); // ok
move(1, 'Nurth'); // Error
```

那 keyof 做的事情就跟 字面量类型一樣，不過是針對型別 key 的部分

```ts
type Person = {
  firsName: string;
  lastName: string;
};

type PersonKey = keyof Person;
```

這時 PersonKey 代表的意思就是: `"firsName" | "lastName"`

實際演練一下:

```ts
interface Person {
    name: string
    age: number
    location: string
}

type SomeNewType = keyof Person

let newTypeObject: SomeNewType
newTypeObject = "name"           // OK
newTypeObject = "age"            // OK
newTypeObject = "location"       // OK
newTypeObject = "anyOtherValue"  // Error
```

## keyof typeof

了解了 keyof 跟 typeof 後，我們來看一下兩者的結合 `keyof typeof`

```ts
const bmw = { name: "BMW", power: "1000hp" }

type CarLiteralType = keyof typeof bmw

let carPropertyLiteral: CarLiteralType
carPropertyLiteral = "name"       // OK
carPropertyLiteral = "power"      // OK
carPropertyLiteral = "anyOther"   // Error
```


### 參考文章

[[Day13] TS：什麼！這個 typeof 和我想的不一樣？](https://pjchender.dev/ironman-2021/ironman-2021-day13/)

[深入理解 TypeScript - 字符串字面量](https://jkchao.github.io/typescript-book-chinese/typings/literals.html#%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%AD%97%E9%9D%A2%E9%87%8F)

[[Day04] TS：如何把物件型別的所有屬性名稱取出變成 union type？試試看 keyof 吧！](https://ithelp.ithome.com.tw/articles/10267302)

[详解 TypeScript 中的 typeof 和 keyof](https://juejin.cn/post/7096869746481561608)

[TypeScript - 简单易懂的 keyof typeof 分析](https://juejin.cn/post/7023238396931735583)