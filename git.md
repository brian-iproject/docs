# GIT

### Работа с ветками ###
Удаление веток из локального репозитория
```
git branch -d <имя_ветки>
```
Для удаления веток, которые уже удалены во внешнем репозитории используйте команду:
```
git remote prune origin
```
Удаление ветки из удаленного Git-репозитория:
```
git push origin --delete <branch_name>
```
Отправить ветку и установить связь с удаленной веткой
```
git push --set-upstream origin develop
```
```
git push -u origin develop
```

### Поведение git push ###
simple - отправлять только текущую ветку (по-умолчанию в GIT 1.*)  
matching - отправлять все ветки (по-умолчанию в GIT 2.*)
```
$ git config --global push.default simple
```

### Общий список параметров ###
```
$ git config --global user.name "Aleksey Pavlov"
$ git config --global user.email brian.iproject@gmail.com
$ git config --global core.editor nano
$ git config --global push.default simple
```