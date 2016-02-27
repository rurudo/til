#鍵設定してもpushできない時
~/.ssh/id_rsaを設定しても何らかの問題で違うパスを解釈する場合がある。
指定の鍵でgit cloneする

```
# git-ssh.sh
exec ssh -i id_rsa "$@"
```

```
GIT_SSH=./git-ssh.sh git clone git@github.com:user_name/repo
```

#参考
http://qiita.com/sonots/items/826b90b085f294f93acf
