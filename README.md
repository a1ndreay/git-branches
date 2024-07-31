# Test branches project
---
<a href="https://t.me/a1ndreay">
  <img src="https://icon-icons.com/icons2/2108/PNG/512/telegram_icon_130816.png" alt="Telegram" width="25" height="25">
</a>

### Simple project for testing __git__ branches

### Используйте `git diff <Назввание 1 ветки> <Название 2 ветки>` для сравнения веток
> [!Tip]
> Так же можно использовать `git diff <Название ветки> <Название коммита>` для сравнения ветки с коммитом


## Переключение между ветками:
#### Чтобы создать ветку введите `git branch <Название ветки>`, к примеру `git branch feature/new-branch-info`
#### Команда `git branch` показывает все доступные ветки
#### Чтобы переключить ветку `git checkout <Название ветки>`
> [!TIP]
> Чтобы просмотреть все ветки, в том числе удалённые, воспользуйтесь `git branch -a`


## Удаление локальных веток
#### Чтобы удалить локальную ветку воспользуйтесь `git branch -d <Название_ветки>`, этой командой следует воспользоваться, если удаляемая ветка уже была влита в текущую актуальную ветку. Иначе воспользуйтесь `git branch -D <Название_ветки>`, эта команда удалит ветку независимо от того, является ли она уже объединённой в актуальную ветку или нет.

## Клонирование удалённого репозитория:
#### Удалённый репозиторий клонируется на локальный компьютер при помощи `git clone git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ_РЕПОЗИТОРИЯ%.git`

## Изменения удалённого репозитория
```bash
$ git remote show
$ git remote get-url origin
http://gitea.praktikum-services.ru/00_student/sausage-store.git
$ git remote set-url origin git@gitlab.praktikum-services.ru:00_student/sausage-store.git
$ git remote get-url origin
git@gitlab.praktikum-services.ru:00_student/sausage-store.git
```


## Связывание локального и удалённого репозитория:
#### Чтобы связать локальный и удалённый репозитории `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ_РЕПОЗИТОРИЯ%.git`
> [!WARNING]
> Перед связыванием проверьте не связан ли уже локальный репозиторий с удалённым при помощи `git remote -v`, если команда выведет пустые строки, значит можете связывать локальный репозиторий с удалённым. Иначе удалите текущую свзяь при помощи `git remote rm origin` и выполните привязку заного.


## Связывание локальной и удалённой веток:
#### Чтобы отправить в удалённый репозиторий новую ветку `git push -u origin <Название ветки>`
#### *Данная команда отправляет текущую ветку в удалённый репозиторий и сразу же связывает её с локальной веткой*
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

## Стягивание изменений:
#### Изменения из удалённого репозитория стягиваются с помощью `git pull`

## FAST-FORWARD
#### Если при слиянии главная ветка может без конфликтов достичь состояния сливаемой ветки, то применимо слияние `fast-forward`, при таком слиянии исходная ветка будет дополнена коммитами сливаемой ветки, как будто этой ветки и не было.
### Изобразим ветки `main` и `add-docs` схематически:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_01_1689342594.png" alt="" crossorigin="anonymous" class="image image_expandable">

#### При таком слиянии, ветку `main` можно довести до состояния ветки `add-docs` дополнив двумя коммитами:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_02_1689342662.png" alt="" crossorigin="anonymous" class="image image_expandable">

> [!WARNING]
> При таком слиянии ветка `add-docs` просто совмещается с веткой `main` как будто её и не было.

## MERGE COMMIT
#### Слияние `fast-forward` можно отключить, добавив следующий флаг: `git merge --no-ff <Название_ветки>`, в таком случае в ветке `main` будет создан дополнительный коммит слияния: 
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_03_1689342784.png" alt="" crossorigin="anonymous" class="image image_expandable">

#### *При таком слиянии будет создан соответствующий коммит:*
```bash
*   6814789 (HEAD -> main) Merge branch 'add-docs'
```
> [!TIP]
> Многие проекты отключают __fast-forward__ слияние веток, потому что при нём теряется часть информации. Результат выглядит так, как будто в `main` «просто появились» новые коммиты. Если не знать о ветке `add-docs`, то можно подумать, что такой ветки и не было.

## NON-FAST-FORWARD
#### Если после отделения новой ветки от целевой, в целевой появился хоть один новый коммит, то в таком случае теоретически возможен конфликт, а новая не может считаться продолжением. В таком случае слияние `fast-forward` невозможно. Схематически это можно изобразить слудующим образом:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_02203_1689343586.png" alt="" crossorigin="anonymous" class="image image_expandable">

#### *При слиянии не `fast-forward` веток будет создан коммит слияния* __merge commit__, слияние либо будет проведено автоматически, либо попросит ручного слияния

> [!TIP]
> Чаще всего сообщения к коммитам слияния не редактируют и оставляют «как предложил Git». Для таких случаев удобен флаг `--no-edit: git merge --no-edit <Название_ветки>`.

## GIT PUSH
#### При выталкивании изменений на сервер может произойти такая же ошибка, что ветка на сервере была изменена, и локальная отстаёт о неё, в таком случае произоёдёт ошибка:
```bash
# текущая ветка — main
$ git push
To github.com:username/repository.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'github.com:username/repository.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
#### Обойти эту ошибку так же можно с помощью `rebase`:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_04202_1689675621.png" alt="" crossorigin="anonymous" class="image image_expandable">

#### Или с помощью __git push --force__, рассмотрим слудующую ситуацию:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_03201_1689593400.png" alt="" crossorigin="anonymous" class="image image_expandable">

#### *Из-за коммита D ветки находятся в состоянии non-fast-forward* В этом случае команда `git push --force` просто «выкинет» (удалит) коммит `D` и запишет в `main@origin` коммиты из `main`. Вот что получится:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T2_00_1689593419.png" alt="" crossorigin="anonymous" class="image image_expandable">

> [!TIP]
> В очень редких случаях это уместная команда. Например, если кто-то нечаянно «сломал» ветку main@origin, можно найти копию репозитория, в которой ветка main не «сломана», и использовать git push --force для восстановления ветки в origin.


# Подходы к работе с ветками
---
## Подход __Feature branch workflow__:
### Основные правила:
1. новая функциональность или исправление — новая ветка;
2. когда код в feature-ветке готов, он вливается в __main__;
3. в __main__ всегда рабочая версия без «недоделок».
4. __main__ состоит только из __merge commit__! 
5. В __main__ запрещен прямой __push__
### Подход обеспечивает:
1. Не будет проблемы «расхождения» веток, ведь новые изменения попадают в __main__ через `git merge`, а не через `git push`. Команду merge «разошедшиеся» ветки не смущают, ведь для них она и придумана.
2. В ветке main всегда рабочая версия проекта.

# Pull-request aka Merge-request aka PR and MR
---
### Данные методы наследуются от подхода  __Feature branch workflow__, обеспечивают, что в __main__ код будет попадать через merge коммиты, которые github делает автоматически.



# Mergetool
---
### При конфликте слияния можно использовать `git mergetool` который создаст копию файла с маркерами изменений, либо воспользоваться VS Code.  


# Проблемы при Pull-request
---
##### Случай: в момент времени __t1__ вы сделали `git checkout -b feature/my-new-awesome-code`, в тот же момент времени __t1__ ваш коллега сделал `git checkout -b feature/other-colleague-code`, в момент времени __t2__ ветка вашего коолеги `feature/other-colleague-code` была влита в ветку `main`:
<img src="https://pictures.s3.yandex.net:443/resources/M4_T4_02201_1689627442.png" alt="" crossorigin="anonymous" class="image image_expandable" style="">  


##### В таком случае ваша удалённые ветка `feature/my-new-awesome-code` и `main`  считаются `non-fast-forward` из-за коммита слияния __t2__. При таком условии GitHub не позволит продолжать Pull-request пока ваш код содержит неразрешимые конфликты. Перейдите локально в главную ветку `git checkout [main|master]` обновите ветку до актуального состояния `git pull`, теперь локально перейдите в вашу ветку `git checkout feature/my-new-awesome-code` выполните слияние с ветокой `main` с целью обновления вашего кода и устранения конфликтов локально `git merge main` и оттправле изменения на github `git push`. Теперь новый коммит с актуальной версией добавится к вашему __Pull-request__ и вы сможете выполнить автоматическое слияние с __main__:

<img src="https://pictures.s3.yandex.net:443/resources/M4_T4_06-2_1689627557.png" alt="" crossorigin="anonymous" class="image image_expandable">  

## Просмотр патчей коммитов
---
#### Каждый коммит вносит в код ряд изменений называемых патчем `git log -p [-2]` флаг __-p__ говорит вывести патчи, влаг __-2__ говорит вывести только 2 последних коммита 

## Просмотр статистики 
---
#### Для удобного просмтра статистики про проделананной работе `git log --since=1.weeks --oneline --stat`
[image.png](https://postimg.cc/LgP9HwJt) 

## Смешные команды __GIT__
---
#### Изменение индекса в интерактивном режиме `git add -i` 
#### Просмотр индексированных файлов `git diff --cached`

#### Припрятать изменения `git stash push`
#### Восстановить припрятанные изменения в индекс `git stash apply --index`
#### Просмотр лога с патчами `git log -p -2` где __-2__ обозначает вывести только 2 последних коммита

## Грустные команды __GIT__
---
#### Извлечь содержимое объекта `git cat-file -p [SHA-1]` где __-p__ автоматичсеки определить тип объекта 

✍️ *Author: Andrey*
