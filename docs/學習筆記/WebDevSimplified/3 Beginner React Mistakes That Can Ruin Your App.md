# 3 Beginner React Mistakes That Can Ruin Your App

<iframe width="100%" height="500" src="https://www.youtube.com/embed/oc_TNtCe2sY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

這部影片提出了三個會影響 React 開發者開發的問題，個人覺得他講的非常的好

## Mistake 1 React onClick 的使用

在 React 中 onClick 三種形式

```js
onClick={handleChange}

onClick={()=>handleChange()}

onClick={handleChange()}
```

這三種的使用情境都不相同，不過還是可以共用

###  onClick={handleChange}

第一種是使用在如果只需要接收 `event` 的值時所使用的，不過也可以寫成:

```js
onClick={e => handleChange(e)}
```

### onClick={()=>handleChange()}

這種寫法是當你執行的 function 有需要接收參數時所使用

### onClick={handleChange()}

最後一種寫法跟其他兩種不一樣的是: 他會在觸發之前就會執行，說清楚一點就是他會在 `render` 期間就執行完畢，且點擊按鈕以後不會有任何反應，因為他沒有 `return` 的值

雖然說如果要接收參數時要使用第二種寫法，不過也不是沒解決的方法，只要 return 一個 function 即可，寫法如下:

```js
const App = () => {

  const handleChange = () => {
    return ()=>{
      console.log('點擊事件發生')
    }
  }

  return (
    <button onClick={handleChange()}>點擊我</button>
  )
}

export default App
```


## Mistake 2: 誤用 &&

我們常常會使用 `&&` 來做判斷 (如果不知道 `&&` 的話可以看[這篇文章](https://medium.com/johnny%E7%9A%84%E8%BD%89%E8%81%B7%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%AD%86%E8%A8%98/js%E5%9F%BA%E7%A4%8E-%E9%82%8F%E8%BC%AF%E9%81%8B%E7%AE%97%E5%AD%90-%E5%92%8C-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8-b590515efed0))

`&&` 這個語法本身非常得直覺，如果左邊的判斷是 `truthy`，就執行右邊程式碼，反之，不執行

```js
x && y 
```

會造成 falsy 的有這些:

```js
console.log(Boolean(false)) // false
console.log(Boolean(0)) // false
console.log(Boolean(‘’)) // false
console.log(Boolean(null)) // false
console.log(Boolean(undefined)) // false
console.log(Boolean(NaN)) // false
```

這邊作者提到的部分就是，如果今天右邊需要判斷得程式碼是數字的話，要特別注意，因為在這邊 0 不會擋掉，會直接在畫面上顯示

```js
const a = []

a.length && (
    <div>{a[0]}</div>
)
```

這邊畫面上會顯示 `0`

## Mistake 3: 使用錯誤的方法去更新 useState

在 React 中，如果要對於 `Array` 或是 `Object` 做更新的話，不能直接修改 state，因為這樣修改的記憶體位置是一樣的，所以就不會觸發 render 。

如果希望可以修改 `Array` 或是 `Object`，必須要做到 `immutable`

要達到 `immutable` 我們需要先複製一份出來，不能更改原本的 state ，常見的複製方法就是 ES6 的 解構

```js
this.setState({ 
  list: [
    ...this.state.list,
    { id: Math.random(), name: randomStr.genreate(4) }
  ]
});
```



### 參考文章

[寫 React 的時候常常聽到 immutable，什麼是 immutable ?](https://medium.com/reactmaker/%E5%AF%AB-react-%E7%9A%84%E6%99%82%E5%80%99%E5%B8%B8%E5%B8%B8%E8%81%BD%E5%88%B0-immutable-%E4%BB%80%E9%BA%BC%E6%98%AF-immutable-146d919f67e4)

[is it possible to React.useState(() => {}) in React?](https://stackoverflow.com/questions/55621212/is-it-possible-to-react-usestate-in-react)