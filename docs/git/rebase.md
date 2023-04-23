# rebase 

rebase 用途很多
1. re-BASE
![rebase](https://res.cloudinary.com/practicaldev/image/fetch/s--EIY4OOcE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/dwyukhq8yj2xliq4i50e.gif)

2. interactive rebase

語法:
```js
git rebase -i 4a16df
```

-i 就是 interactive 的意思

裡面有幾種方法可以自己選擇
- reword: Change the commit message
- edit: Amend this commit
- squash: Meld commit into the previous commit
- fixup: Meld commit into the previous commit, without keeping the commit's log message
- exec: Run a command on each commit we want to rebase
- drop: Remove the commit


interactive rebase 開啟的是 vim 編輯器
esc 是鎖定鍵盤，所以要編輯時請先開啟鍵盤
編輯是 i 
要退出請先點擊 esc 確定鍵盤已鎖
然後輸入 :wq, :w, :q

- wq 儲存加退出
- w 儲存
- q 退出

