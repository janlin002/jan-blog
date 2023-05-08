# day4: Apply Transform Over Each Element in Array

## 題目

Given an integer array `arr` and a mapping function `fn`, return a new array with a transformation applied to each element.

The returned array should be created such that `returnedArray[i] = fn(arr[i], i)`.

Please solve it without the built-in `Array.map` method.

```js
Input: arr = [1,2,3], fn = function plusone(n) { return n + 1; }
Output: [2,3,4]
Explanation:
const newArray = map(arr, plusone); // [2,3,4]
The function increases each value in the array by one. 
```

```js
Input: arr = [1,2,3], fn = function plusI(n, i) { return n + i; }
Output: [1,3,5]
Explanation: The function increases each value by the index it resides in.
```

```js
Input: arr = [10,20,30], fn = function constant() { return 42; }
Output: [42,42,42]
Explanation: The function always returns 42.
```

## 解答

這題是會有三種 function：
1. plusone
2. plusI
3. constant

照著題目的 `returnedArray[i] = fn(arr[i], i)` 去寫就會對了

```js
/**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
var map = function(arr, fn) {
    const newMap = []
    for(let i = 0; i < arr.length; i++){
        newMap[i] = fn(arr[i], i)
    }

    return newMap
};
```