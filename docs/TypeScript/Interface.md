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