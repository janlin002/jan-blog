# throttle-debounce

[套件Github位置](https://github.com/niksy/throttle-debounce)

## 如何使用？

### Throttle

```js
import { throttle } from 'throttle-debounce';

const throttleFunc = throttle(
	1000,
	(num) => {
		console.log('num:', num);
	},
	{ noLeading: false, noTrailing: false }
);
```

或是可以寫成(`noLeading` 跟 `noTrailing` 預設都是 `false`)

```js
const throttleFunc = throttle(1000, (num) => {
	console.log('num:', num);
});
```

### Debounce

```js
import { debounce } from 'throttle-debounce';

const debounceFunc = debounce(
	1000,
	(num) => {
		console.log('num:', num);
	},
	{ atBegin: false }
);
```

atBegin 預設就是 false ，所以可以寫成

```js
const debounceFunc = debounce(1000, (num) => {
	console.log('num:', num);
});
```

### Cancelling

不管 Throttle 還是 Debounce，都能使用 Cancelling，可以取消掉 funciton 的執行

```js
const throttleFunc = throttle(300, () => {
	// Throttled function
});

throttleFunc.cancel();

const debounceFunc = debounce(300, () => {
	// Debounced function
});

debounceFunc.cancel();
```

如果只想要取消掉一次的話，可加上 `upcomingOnly: true`

```js
const debounceFunc = debounce(300, () => {
	// Debounced function
});

debounceFunc.cancel({ upcomingOnly: true });
```

## 原始碼部分

### throttle

```js
export default function (delay, callback, options) {
  const {
    noTrailing = false,
    noLeading = false,
    debounceMode = undefined
  } = options || {}

  let timeoutID
  let cancelled = false
  let lastExec = 0

  function clearExistingTimeout() {
    if (timeoutID) {
      clearTimeout(timeoutID)
    }
  }

  function cancel(options) {
    const { upcomingOnly = false } = options || {}
    clearExistingTimeout()
    cancelled = !upcomingOnly
  }

  function wrapper(...arguments_) {
    let self = this
    let elapsed = Date.now() - lastExec

    if (cancelled) {
      return
    }

    function exec() {
      lastExec = Date.now()
      callback.apply(self, arguments_)
    }

    function clear() {
      timeoutID = undefined
    }

    if (!noLeading && debounceMode && !timeoutID) {
      exec()
    }

    clearExistingTimeout()

    if (debounceMode === undefined && elapsed > delay) {
      if (noLeading) {
        lastExec = Date.now()
        if (!noTrailing) {
          timeoutID = setTimeout(debounceMode ? clear : exec, delay)
        }
      } else {
        exec()
      }
    } else if (noTrailing !== true) {
      timeoutID = setTimeout(
        debounceMode ? clear : exec,
        debounceMode === undefined ? delay - elapsed : delay
      )
    }
  }

  wrapper.cancel = cancel

  return wrapper
}
```

### debounce

```js
import throttle from './throttle'

export default function (delay, callback, options) {
  const { atBegin = false } = options || {}
  return throttle(delay, callback, { debounceMode: atBegin !== false })
}
```