# TypeScript 學習筆記

### 為什麼需要 TypeScript？

因為 JavsScript 是弱型別的語言，也因為這樣型別可以換來換去，增加了發生錯誤的機率，TypeScript 就是為了解決這樣的問題，透過 TypeScript 我們需要嚴格定義型別的部分，減少出錯的機會

### 聯集 (Union)

讓我們可以不侷限於一個特定型別

```js
let age: number | string
```

### 型別防衛 (Type Guard)

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

### 型別斷言 (Type Assertion)

类型断言（Type Assertion）可以用来手动指定一个值的类型。

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
    if (typeof animal.swim === 'function') {
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

[型別介紹part3 - 型別斷言](https://ithelp.ithome.com.tw/articles/10295260)

### 型別別名 (Type Alise)

我們可以將特定組合的型別，給安上一個別名，方便我們後續使用，成為一個新的type

### Interface（介面）

不能拿來指涉聯集、原始值、或其他型別。

跟type最大的不同應該是這點：interface可以一直被擴充。

TypeScript會直接將同樣名稱的interface合而為一，不過前提是這當中沒有重複／衝突的屬性

若要更明確的"擴充"介面，則可以透過關鍵字extends來擴充

```js
interface Animal {
    name: string
}

interface Bear extends Animal {
    honey: boolean
}

// 這邊的Bear就從Animal擴充了honey屬性
const bear: Bear = {
    honey: true,
    name: "Winnie"
}
```

如果type想要"擴充"，須透過 `&`

```js
type Rice = {
    name: string
}
type RiceWithPrice = Rice & {
    price: number
}

let friedRice: RiceWithPrice = {
    name: "Yangzhou fried rice", price: 140
}
```

我們可以混著使用型別別名與介面

```js
interface Name {
    name: string
};

interface Age {
    age: number
};

type Person = Name & Age;

let guy: Person = {
    name: "John",
    age: 18
}
```

### unknown

不確定的情況

unknown vs any??

any 完全不會做判斷，即使出錯

### never

"絕不"會被回傳／執行

### void

void代表的是「函式沒有回傳任何值」，不是沒有return，是沒有回傳任何值。

### 選擇性屬性 vs 唯讀屬性

#### 選擇性屬性

有點像三元的 `?`

寫法就是在 變數的右邊加上 `?`

```js
interface FriedRice {
    name: string
    price: number
    ingredients?: string[]
}

//沒有ingredients也不會報錯
const dish: FriedRice = {
    name:"Yanzhou fried rice",
    price:120,
}
```

#### 唯讀屬性(readonly)

代表這個變數是: 唯讀而不能/不該被改變的

寫法就是在變數前面加上 `readonly`

```js
interface Person {
    readonly name: string
    age: number
}

const John: Person = {
    name: "John",
    age: 18
}

// Cannot assign to 'name' because it is a read-only property.
John.name = "Allen"
```


