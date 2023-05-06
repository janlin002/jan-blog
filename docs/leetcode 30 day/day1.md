# day1: Create Hello World Function

## 題目
```js
/**
 * @return {Function}
 */
var createHelloWorld = function() {
    return function(...args) {
    }
};

/**
 * const f = createHelloWorld();
 * f(); // "Hello World"
 */
```

## 解答

就是簡單的回傳 `"Hello World"` 即可

```js
var createHelloWorld = function() {
    return function(...args) {
        return 'Hello World'
    }
};
```