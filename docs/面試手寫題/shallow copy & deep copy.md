# JavaScript 淺拷貝 (shallow copy) 和深拷貝 (deep copy)

## 什麼是 淺拷貝 (shallow copy) 和深拷貝 (deep copy) ？

淺拷貝是指複製值時，原本的變數和新的變數會指向同一個址 (reference)，換句話說，如果拷貝的物件內容有改變，原本的物件也會被改變。反之，深拷貝就是複製值以後，兩者已經完全沒有關係，一方有所變更，也不會影響另外一方

深拷貝在生活中的例子: 影印，今天我影印兩份作業，一份給小華一份給我自己，如果小華在作業中有所更改，也不會影響我的成績

```js
let objA = {
  a: 1,
  b: 2,
};

let objB = objA;

objB.a = 3; // 因為是淺拷貝，objA 的 a 也會被改變

console.log(objA); //{a:3, b:2}
console.log(objB); //{a:3, b:2}
```

```js
// lodash 的淺拷貝 clone
var objects = [{ a: 1 }, { b: 2 }];
var shallow = _.clone(objects);
console.log(objects === shallow); // false
console.log(shallow[0] === objects[0]); // true

// lodash 的深拷貝 cloneDeep (完全不同的兩個 object)
var objects = [{ a: 1 }, { b: 2 }];
var deep = _.cloneDeep(objects);
console.log(objects === deep); // false
console.log(deep[0] === objects[0]); // false
```

## 實作 淺拷貝 (shallow copy) 和深拷貝 (deep copy)

### **淺拷貝 (shallow copy)**

1. 方法一：手動複製值

```js
let objA = {
  a: 1,
  b: { c: 3 },
};

let objB = { a: objA.a, b: objA.b };

console.log(objA === objB); // false
console.log(objA.b === objB.b); // true, 第二層的物件還是指向相同位置
```

2. 使用 spread syntax

```js
let objA = {
  a: 1,
  b: { c: 3 },
};

let objB = { ...objA };

console.log(objA === objB); // false
console.log(objA.b === objB.b); // true, 第二層的物件還是指向相同位置
```

3. Object.assign

```js
let objA = {
  a: 1,
  b: { c: 3 },
};

let objB = Object.assign({}, objA);

console.log(objA === objB); // false
console.log(objA.b === objB.b); // true, 第二層的物件還是指向相同位置
```

### **深拷貝 (deep copy)**

1. JSON.parse(JSON.stringify(...))
這個作法是先將物件用 JSON.stringify 序列化為 string，再透過 JSON.parse 轉換回物件。

```js
let objA = {
  a: 1,
  b: { c: 3 },
};

function deepCopy(item) {
  return JSON.parse(JSON.stringify(item));
}

let objB = deepCopy(objA);

console.log(objA === objB); // false
console.log(objA.b === objB.b); // false
```

2. structuredClone(value)

```js
let objA = {
  a: 1,
  b: { c: 3 },
};

let objB = structuredClone(objA);

console.log(objA === objB); // false
console.log(objA.b === objB.b); // false
```
## 參考資料

[請實踐 JavaScript 淺拷貝 (shallow copy) 和深拷貝 (deep copy)](https://www.explainthis.io/zh-hant/interview-guides/javascript-whiteboard/shallow-copy-and-deep-copy)