# Symbol

## 什麼是 Symbol ?

Symbol 是 ES6 新推出的資料型別，表示`獨一無二(unique) `的值，

什麼叫獨一無二？在 ES5 中，object 的屬性 (property) 只能是字串，如果你要幫一個 object 添加新的屬性，很容易會造成名稱衝突，Symbol 就是用來解決這件事情的。

## 如何使用 ?

需要注意的是 `Symbol` 前面不用加上 `new`
```js
let s1 = Symbol();

// "symbol"
typeof s1;

let s2 = Symbol();

// false
s1 === s2;
```

```js
let s1 = Symbol('foo');

// 建立一個和 s1 同名的 s2
let s2 = Symbol('foo');

// 雖然同名，但 s1 和 s2 還是不一樣的值
// false
s1 === s2;
```

## 使用情境

由於每個 Symbol 值都是不相等的，所以用 Symbol 來當作物件的屬性名稱，可以確保不會出現同名的屬性，這特性能防止一個物件的屬性不會在其他地方被意外的覆蓋掉。

```js
var mySymbol = Symbol();

// 下面三種寫法都可以定義一個 Symbol 屬性名稱

// 寫法 1
var a = {};
a[mySymbol] = 'Hello!';

// 寫法 2
var a = {
    [mySymbol]: 'Hello!'
};

// 寫法 3
var a = {};
Object.defineProperty(a, mySymbol, {value: 'Hello!'});

// "Hello!"
a[mySymbol];
```

### Symbol.for() / Symbol.keyFor()

有時候，你會希望重複利用同一個 Symbol 值，你可以用 Symbol.for() 和 Symbol.keyFor() 來存取全域的 Symbol 值

- Symbol.for(key) 用來取得名稱為 key (字串) 的 global Symbol，如果不存在則會先建立一個新的存到 global symbol registry 後再返回

```js
// 建立一個 global Symbol
Symbol.for('foo');

// 不會再重複建立，會直接返回已經建立的 Symbol
Symbol.for('foo');

// true
Symbol.for('bar') === Symbol.for('bar');

// false
Symbol('bar') === Symbol('bar');

// key 名稱也會被當成 Symbol 名稱
var sym = Symbol.for('mario');
// "Symbol(mario)"
sym.toString();
```

- Symbol.keyFor(sym) 用來取得某個 global Symbol 的 key 名稱

```js
var globalSym = Symbol.for('foo');

// "foo"
Symbol.keyFor(globalSym);

var localSym = Symbol();
// 如果沒有這個 global Symbol 會返回 undefined

// undefined
Symbol.keyFor(localSym);
```

### 調用

Symbol 的屬性名稱不能被遍歷，像是 for...in, for...of, Object.keys(), Object.getOwnPropertyNames(), JSON.stringify() 都不會返回 Symbol 屬性名。

你要取得所有的 Symbol 屬性名稱可以使用 `Object.getOwnPropertySymbols()` 或是 `Reflect.ownKeys()` 方法，該方法會返回一個陣列。

```js
ar obj = {
  name: 'Aaron',
};
var a = Symbol('aaa');
var b = Symbol('bbb');

obj[a] = 'Hello';
obj[b] = 'World';

/**
 * obj
 * {
 *   name: "Aaron",
 *   Symbol(aaa): "Hello",
 *   Symbol(bbb): "World"
 * }
 **/

/**
 * 可以取得 Symbols 的方式
 **/

// 使用 Object.getOwnPropertySymbols() 取得物件的 Symbol
Object.getOwnPropertySymbols(obj); // [Symbol(a), Symbol(b)]

// 使用 Reflect.ownKeys() 取得物件所有的 key
Reflect.ownKeys(obj); // ["name", Symbol(aaa), Symbol(bbb)]

/**
 * 無法取得 Symbols 的方式
 **/

// 無法使用 Object.keys() 取得 Symbol
Object.keys(obj);

// 無法使用 for...in 取得 Symbol
for (let prop in obj) {
  console.log(`${prop}: ${obj[prop]}`); // name: Aaron
}

// 無法使用 Object.getOwnPropertyNames() 取得 Symbol
Object.getOwnPropertyNames(obj); // ['name']
```



#### 參考資料

[[JS] Symbols 的使用](https://pjchender.dev/javascript/js-symbols/)

[JavaScript ES6 Symbol 資料型態](https://www.fooish.com/javascript/ES6/Symbol.html)

[Day24【ES6 小筆記】資料型別 Symbol 使用時機](https://ithelp.ithome.com.tw/articles/10220499)