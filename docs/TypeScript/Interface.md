# Interface（介面）

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

### 可選屬性

有時我們希望不要完全匹配一個形狀，那麼可以用可選屬性 (?)

> 可選屬性的含義是該屬性可以不存在。

```ts
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```

### 任意屬性

有時候我們希望一個介面允許有任意的屬性

需要注意的是，`一旦定義了任意屬性，那麼確定屬性和可選屬性的型別都必須是它的型別的子集`

```ts
interface Person {
    name: string;
    age?: number;
    [propName: string]: string;
}

let tom: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};
```

上方程式碼會報錯，因為 number(age) 不是 string([propName: string]) 的子集

> 子集: B 裡面包涵 A，那麼 A 就是 B 的子集

[子集維基百科](https://zh.wikipedia.org/zh-tw/%E5%AD%90%E9%9B%86)

### 唯讀屬性

有時候我們希望物件中的一些欄位只能在建立的時候被賦值，那麼可以用 readonly 定義唯讀屬性

```ts
interface Person {
    readonly id: number;
    name: string;
    age?: number;
}

let tom: Person = {
    id: 89757,
    name: 'Tom',
};

tom.id = 9527;
```

這樣會報錯的原因是因為 id 是唯獨屬性，所以不能賦值

### 參考資料

[物件的型別——介面](https://willh.gitbook.io/typescript-tutorial/basics/type-of-object-interfaces)