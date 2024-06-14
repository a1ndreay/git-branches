# Test branches project
---
### Simple project for testing __git__ branches

### Используйте `git diff <Назввание 1 ветки> <Название 2 ветки>` для сравнения веток
> [!Tip]
> Так же можно использовать `git diff <Название ветки> <Название коммита>` для сравнения ветки с коммитом


## Переключение между ветками:
#### Чтобы создать ветку введите `git branch <Название ветки>`, к примеру `git branch feature/new-branch-info`
#### Команда `git branch` показывает все доступные ветки
#### Чтобы переключить ветку `git checkout <Название ветки>`


## Связывание локального и удалённого репозитория:
#### Чтобы связать локальный и удалённый репозитории `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ_РЕПОЗИТОРИЯ%.git`


## Связывание локальной и удалённой веток:
#### Чтобы отправить в удалённый репозиторий новую ветку `git push -u origin <Название ветки>`
> [!WARNING]
> Ветка с таким именем не должна существовать в удалённом репозитории, этой командой вы отправляете и связываете локальную ветку на удалённый репозиторий.


## __Алгоритм работы на локальной ветке__
#### *Так как остальные разработчики вливают изменения в ветку __main__, перед созданием пул-реквеста __необходимо__ перейти в главную актуальную ветку, стянуть в неё все изменения с удалённого репозитория, перейти в вашу локальную ветку и выполнить в неё __merge__ ветки __main__ чтобы заранее устранить всевозможные конфликты самим!*
```bash
$ git checkout main # перешли в main
$ git pull # подтянули новые изменения в main
$ git checkout my-branch # вернулись в рабочую ветку my-branch
$ git merge main # влили main в новую ветку my-branch
$ git push -u origin my-branch # отправили ветку my-branch в удалённый репозиторий
```


✍️ *Author: Andrey*
