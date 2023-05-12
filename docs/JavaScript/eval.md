# .eval()

JavaScript eval 函數是個功能非常強大的函數，eval 函數可以執行某一段字串（String）的運算，如果該字串是運算式，則 eval 會計算出運算結果，如果只是單純數個字串的連接，eval 會自動返回組和好的整個字串

## eval() 基礎用法

```js
eval( 要執行的字串 )
```

如果未填值，會回傳 `undefined`

## 實際使用

```js
eval('2 + 2')
// 4

const employee = {
  name: 'jan',
  age: 100,
  job: {
    name: 'front end development'
  }
}
eval('var { name, age, job } = employee')
console.log(name, age, job) // 'jan' 100 front end development
```

#### 參考文章:

[Interviewer: Can You Implement a JavaScript Template Engine? Me: Crap…](https://fatfish.medium.com/interviewer-can-you-implement-a-javascript-template-engine-me-crap-e195963b4546)

[JavaScript eval() 函數](https://www.wibibi.com/info.php?tid=264)

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/eval)