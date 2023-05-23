# 泛型Generic Types

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