# 既存のディレクトリをgit管理にしてリモートリポジトリと紐づけ
```
$ git init
$ git remote add origin ${git url}
$ git add .
$ git commit -m 'first commit'
$ git push --set-upstream origin master
```

# git add を取り消す
## git init 直後のgit addを取り消したい場合
```
$ git rm --cached -r .
```
or
```
$ git rm --cached -r ${file_name}
```
## 2回目以降のgit add を取り消す
```
$ git reset HEAD
```
or
```
$ git reset HEAD ${file_name}
```

# 特定のディレクトリだけgit cloneする
```
$ git init
$ git config core.sparsecheckout true
$ git remote add origin ${URL}
$ git sparse-checkout set ${DIRECTORY_NAME}
$ git pull origin ${BRANCH_NAME}
```

# パスワードなどが入ったセンシティブなファイルをpushしてしまったときの対処法
## gitの履歴から該当のファイルを消す
```
$ git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch ${file_name}' -- --all
$ git push -f origin ${branch_name}
```

- git filter-branch : Gitの歴史をまとめて書き換えるコマンド
- --force : filter-branchを強制的に実行するオプション
- --index-filter : local repositoryに保存されたファイルをindex上で書き換えるオプション
- git rm : indexとwoking treeからファイルを削除するコマンド
- --cached : indexのみから削除するオプション
- --ignore-unmatch : ファイルが存在しなくてもそのまま実行するオプション
- -- : 実行されるコミットの範囲を指定するオプション。今回は「--all」を指定

## ローカルリポジトリから完全に痕跡を消す
```
$ rm -rf .git/refs/original/
$ git reflog expire --expire=now --all
$ git gc --aggressive --prune=now
```