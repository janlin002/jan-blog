# day5: Filter Elements from Array

## 題目

Given an integer array arr and a filtering function fn, return a new array with a fewer or equal number of elements.

The returned array should only contain elements where fn(arr[i], i) evaluated to a truthy value.

Please solve it without the built-in `Array.filter` method.

```js
Input: arr = [0,10,20,30], fn = function greaterThan10(n) { return n > 10; }
Output: [20,30]
Explanation:
const newArray = filter(arr, fn); // [20, 30]
The function filters out values that are not greater than 10
```

```js
Input: arr = [1,2,3], fn = function firstIndex(n, i) { return i === 0; }
Output: [1]
Explanation:
fn can also accept the index of each element
In this case, the function removes elements not at index 0
```

```js
Input: arr = [-2,-1,0,1,2], fn = function plusOne(n) { return n + 1 }
Output: [-2,0,1,2]
Explanation:
Falsey values such as 0 should be filtered out
```

## 解答

這題是希望可以將符合 `fn` 條件的值留下來，不過在題目最後有提到不能使用 `filter`

所以我們會需要自己建立一個 `array`，將符合條件的部分加入

```js
/**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
var filter = function(arr, fn) {
    const ansArr = []
    for(let i = 0; i < arr.length; i++){
        const test = fn(arr[i], i)
        if(test){
            ansArr.push(arr[i])
        }
    }
    return ansArr
};
```