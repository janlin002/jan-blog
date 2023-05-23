# useState

```ts
const [count, setCount] = useState<string | number>(0)

const onClick = () => {
    setCount("no count")
}
```

如果 state 是物件的話，可以這樣寫

```ts
interface Count {
  value: number
}

function App() {
  const [count, setCount] = useState<Count | null>({ value: 0 })
  const onClick = () => {
    setCount(null)
  }

  return (
    <div className="App">
      <span>{count && count.value}</span>
      <button onClick={onClick}>Hi</button>
    </div>
  )
}
```