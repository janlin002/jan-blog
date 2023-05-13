# day7: Function Composition

## 題目

Given an array of functions [f1, f2, f3, ..., fn], return a new function fn that is the function composition of the array of functions.

The function composition of [f(x), g(x), h(x)] is fn(x) = f(g(h(x))).

The function composition of an empty list of functions is the identity function f(x) = x.

You may assume each function in the array accepts one integer as input and returns one integer as output.

```js
Input: functions = [x => x + 1, x => x * x, x => 2 * x], x = 4
Output: 65
Explanation:
Evaluating from right to left ...
Starting with x = 4.
2 * (4) = 8
(8) * (8) = 64
(64) + 1 = 65
```

```js
Input: functions = [x => 10 * x, x => 10 * x, x => 10 * x], x = 1
Output: 1000
Explanation:
Evaluating from right to left ...
10 * (1) = 10
10 * (10) = 100
10 * (100) = 1000
```

```js
Input: functions = [], x = 42
Output: 42
Explanation:
The composition of zero functions is the identity function
```

## 解答

這題是在考 js 的 compose => fn(x) = f(g(h(x)))，首先我們須先將 functions 裡面的行為獨立出來(這邊需要注意一下，因為是由後方開始執行，所以要先將 functions 反轉過來)，並且將 x 一個個帶入，取得加總

不過在開始前有提到，如果 functions 是 empty array 的話，直接回傳 x 即可，所以剛開始會先做一波篩選

```js
/**
 * @param {Function[]} functions
 * @return {Function}
 */
var compose = function(functions) {
	return function(x) {
    if (functions.length === 0) return x;
    let input = x;

    for (const func of functions.reverse()) {
      input = func(input);
    }

    return input;
    }
};

/**
 * const fn = compose([x => x + 1, x => 2 * x])
 * fn(4) // 9
 */
```
