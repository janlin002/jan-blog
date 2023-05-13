# day6: Array Reduce Transformation

## 題目

Given an integer array nums, a reducer function fn, and an initial value init, return a reduced array.

A reduced array is created by applying the following operation: val = fn(init, nums[0]), val = fn(val, nums[1]), val = fn(val, nums[2]), ... until every element in the array has been processed. The final value of val is returned.

If the length of the array is 0, it should return init.

Please solve it without using the built-in `Array.reduce` method.

```js
Input: 
nums = [1,2,3,4]
fn = function sum(accum, curr) { return accum + curr; }
init = 0
Output: 10
Explanation:
initially, the value is init=0.
(0) + nums[0] = 1
(1) + nums[1] = 3
(3) + nums[2] = 6
(6) + nums[3] = 10
The final answer is 10.
```

```js
Input: 
nums = [1,2,3,4]
fn = function sum(accum, curr) { return accum + curr * curr; }
init = 100
Output: 130
Explanation:
initially, the value is init=100.
(100) + nums[0]^2 = 101
(101) + nums[1]^2 = 105
(105) + nums[2]^2 = 114
(114) + nums[3]^2 = 130
The final answer is 130.
```

```js
Input: 
nums = []
fn = function sum(accum, curr) { return 0; }
init = 25
Output: 25
Explanation: For empty arrays, the answer is always init.
```

## 解答

今天的題目是累加，須將 nums 帶入到 fn 中，並且跟 init 相加，並且不能使用到 Array.reduce

也就是說我們需要建立一個可以累加的變數，並且執行完 fn 需要自動更新

這邊我們將 init 當作預設值，並且在執行完 fn 時，將初始值改成 fn 執行過後的值

```js
/**
 * @param {number[]} nums
 * @param {Function} fn
 * @param {number} init
 * @return {number}
 */
var reduce = function(nums, fn, init) {
     let ans = init;
  for (let i = 0; i < nums.length; i++) {
    ans = fn(ans, nums[i]);
  }
  return ans;
};
```