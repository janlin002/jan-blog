# day9: Memoize

## 題目

Given a function fn, return a memoized version of that function.

A memoized function is a function that will never be called twice with the same inputs. Instead it will return a cached value.

You can assume there are 3 possible input functions: sum, fib, and factorial.

sum accepts two integers a and b and returns a + b.
fib accepts a single integer n and returns 1 if n <= 1 or fib(n - 1) + fib(n - 2) otherwise.
factorial accepts a single integer n and returns 1 if n <= 1 or factorial(n - 1) * n otherwise.

```js
Input
"sum"
["call","call","getCallCount","call","getCallCount"]
[[2,2],[2,2],[],[1,2],[]]
Output
[4,4,1,3,2]
```

```js
Input
"factorial"
["call","call","call","getCallCount","call","getCallCount"]
[[2],[3],[2],[],[3],[]]
Output
[2,6,2,2,6,2]
```

## 解答