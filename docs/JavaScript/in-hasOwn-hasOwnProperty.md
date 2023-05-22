# in vs. hasOwn vs. hasOwnProperty

這篇來講一下 in, hasOwn, hasOwnProperty 這三者的差異，跟為什麼大家推薦使用 hasOwn 取代 hasOwnProperty？

在開始前，我們先要知道這三種方法都可以拿來判斷一個 Object 中是否有特定的屬性，不過在使用上有些微的不同

## in

in 的寫法如下

```js
prop in object
```

實例:

```js
const car = { make: 'Honda', model: 'Accord', year: 1998 };

console.log('make' in car); // true
```

不過 in 有個特性，就是會繼承到 Object 原生的方法，接下來的例子我們可以更清楚這段話是什麼意思

```js
const item = {
    car: 'Honda'
}

console.log('toString' in item) // true
```

console.log 出來會是 `true`，原因是因為 `Object` 中有一個叫 `toString` 的方法，所以才會回傳 `true`

## hasOwn

只有在自己的 `Object` 中有的屬性才會回傳 `true` ，也就是說他不會因為 Object 中有這個方法，所以回傳 true

寫法如下:

```js
const car = { make: 'Honda', model: 'Accord', year: 1998 };

console.log(Object.hasOwn(car, 'make')); // true
console.log(Object.hasOwn(car, 'toString')) // false
```

## hasOwnProperty

hasOwnProperty 主要是用於檢查一個物件內是否有某個屬性存在，如果有就會回傳 true，反之則會回傳 false

寫法也很簡單:

```js
obj.hasOwnProperty('key')
```

既然這麼簡單，但是為什麼大家都不推薦？


1. 會有被覆寫的可能 

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  hasOwnProperty(){
    return false
  },
}

console.log(obj.hasOwnProperty('a')) 
```

(雖然我覺的應該不會有人特別這樣寫...吧？)

2. hasOwnProperty 沒辦法跟 Object.create() 一起使用

當今天我們的 Object 是使用 Object.create() 去建立的話，就不能使用 hasOwnProperty 了

```js
const foo = Object.create(null);
foo.prop = 'exists';

console.log(foo.hasOwnProperty('prop')) // foo.hasOwnProperty is not a function
console.log(Object.hasOwn('prop')) // true
```



### 參考文章

[[JS] 如何判斷物件中是否帶有特定屬性，為什麼要改用 hasOwn 方法？](https://ithelp.ithome.com.tw/articles/10302805)

[為什麼不建議直接使用 hasOwnProperty？](https://israynotarray.com/javascript/20230218/1132871629/)

[Object.create與class](https://ithelp.ithome.com.tw/articles/10195322)


hasOwnProperty 找不到 Object.create() 這個方法
