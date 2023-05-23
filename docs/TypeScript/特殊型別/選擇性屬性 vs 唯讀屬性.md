# 選擇性屬性 vs 唯讀屬性

## 選擇性屬性

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

## 唯讀屬性(readonly)

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