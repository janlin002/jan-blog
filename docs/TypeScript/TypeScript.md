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

### 泛型Generic Types

可以讓使用者在宣告函式或類別時，不用事先宣告好具體的型別，而是等到要呼叫的時候，再把型別帶進去就好了。這就使得我們的函式或類別在使用上更便利、更通用、但又能保有操作上的安全性。

```js
function returnArg(arg:number):number{
    return arg
}

function returnArg<T>(arg:T){
    return arg
}
```

上面的程式碼只能是 number，下面的程式碼可以是任何型別

泛型還能用在interface

```js
interface Person<T> {
  name: string
  age: number
  info: T
}
```

實際用法

```js
interface Person<T> {
  name: string
  age: number
  info: T
}

let john: Person<string> = {
  name: "John",
  age: 18,
  //這邊就會報錯了，會寫string[]不能指派給類型string
  info: ["polite"]
}
let allen: Person<string> = {
  name: "Allen",
  age: 20,
  info: "polite" //正確不報錯
}
```

### 函式重載 (funciton overload)

函數重載（Function Overloading）是一種程式設計技術，它允許開發者在定義函數時，指定不同的參數型別，以及不同的回傳型別。

當我們在 TS 中使用 Unions 時，函式變得很複雜，並且我們會多做很多的判斷

```js
type Combinable = string | number

function add(a: Combinable, b: Combinable): Combinable{
  if(typeof a === 'string' || typeof b === 'string'){
    return a.toString() + b.toString()
  }
  return a + b
}
const result = add(1, 5)
```

這時候會報錯，因為typeScript認為Combinable不具備toString方法，這時候有兩種方式可以解決

1. 型別斷言

這樣可以明確的跟 TS 說，我這邊是要使用 `number`
```js
const result = add(1, 5) as number
```
2. Function Overloads

在 funciton 前面直接對他的型別做定義
```js
function add(a: number, b: number): number
function add(a: string, b: string): string
```


參考文章:

[學習TypeScript中的函數重載：深入了解函數的功能與應用](https://badgameshow.com/steven/typescript/%E5%AD%B8%E7%BF%92typescript%E4%B8%AD%E7%9A%84%E5%87%BD%E6%95%B8%E9%87%8D%E8%BC%89%EF%BC%9A%E6%B7%B1%E5%85%A5%E4%BA%86%E8%A7%A3%E5%87%BD%E6%95%B8%E7%9A%84%E5%8A%9F%E8%83%BD%E8%88%87%E6%87%89%E7%94%A8/)

[TypeScript — Advance Types(上)](https://medium.com/summers-life/typescript-advance-types-9e569b4f6ff2)

[TypeScript — Advance Types(下)](https://medium.com/summers-life/typescript-advance-types-%E4%B8%8B-70a802ceac92)

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

### Tuple 元組

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
### Enum 列舉

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

### 架設一個 TS 專案

首先須先下載 typeScript

```js
yarn add typescript -D
```

然後我們會需要所謂的TS設定檔: `tsconfig.json`

```js
npx tsc --init
```

## TypeScript & React

### useState

```ts
const [count, setCount] = useState<string | number>(0)

const onClick = () => {
    setCount("no count")
}
```

如果 state 是物件的話，可以這樣寫

```ts
interface Count {
  value: number
}

function App() {
  const [count, setCount] = useState<Count | null>({ value: 0 })
  const onClick = () => {
    setCount(null)
  }

  return (
    <div className="App">
      <span>{count && count.value}</span>
      <button onClick={onClick}>Hi</button>
    </div>
  )
}
```