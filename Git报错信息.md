## . 1 
```javaScript
    $ git push -u origin master
    To git@github.com:xxx/xxx.git
    ! [rejected]        master -> master (fetch first)
    error: failed to push some refs to 'git@github.com:xxx/xxx.git'
    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
原因： 
GitHub远程仓库中的README.md文件不在本地仓库中。 
解决方案：

```JavaScript
$ git pull --rebase origin master
$ git push -u origin master
```