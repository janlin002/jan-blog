# reset

Git reset 這個指令用於回退版本，可以指定退回某一次提交的版本。

git reset 格式:

```js
git reset [要還原的行為] [要還原的部分]
```
## 要還原的行為

這邊分成三種行為: `soft`, `mixed`, `hard`

`soft`: 這個模式下的 reset，工作目錄跟暫存區的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已。也因此，Commit 拆出來的檔案會直接放在暫存區。

![git-reset-soft](https://res.cloudinary.com/practicaldev/image/fetch/s---GveiZe---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/je5240aqa5uw9d8j3ibb.gif)

`mixed`: --mixed 是預設的參數，如果沒有特別加參數，git reset 指令將會使用 --mixed 模式。這個模式會把暫存區的檔案丟掉，但不會動到工作目錄的檔案，也就是說 Commit 拆出來的檔案會留在工作目錄，但不會留在暫存區。

`hard`: 使用這個指令時要小心，因為在這個模式下，不管是工作目錄以及暫存區的檔案都會丟掉。

不過如果不小心真的 reset 了一個錯誤的 commit 還是有辦法還原的

https://gitbook.tw/chapters/using-git/restore-hard-reset-commit

## 要還原的部分
有兩種方式可以選擇: hash, HEAD

hash 就不多說了，大家都知道

HEAD 可以理解成目前所在的位置

HEAD^ 代表前一個 commit，也可以寫成 HEAD ~ 1