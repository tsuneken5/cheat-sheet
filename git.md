# 既存のディレクトリをgit管理にしてリモートリポジトリと紐づけ
```
$ git init
$ git remote add origin {git url}
$ git add .
$ git commit -m 'first commit'
$ git push --set-upstream origin master
```

# git add を取り消す
## git init 直後のgit addを取り消したい場合
```
$ git rm --cached -r .
$ git rm --cached -r file_name
```
## 2回目以降のgit add を取り消す
```
$ git reset HEAD
$ git reset HEAD file_name
```

# 特定のディレクトリだけgit cloneする
```
$ git init
$ git config core.sparsecheckout true
$ git remote add origin ${URL}
$ git sparse-checkout set ${DIRECTORY_NAME}
$ git pull origin ${BRANCH_NAME}
```
