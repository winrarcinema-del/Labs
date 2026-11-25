# Лабораторная работа 9. Git

Студент: [Фамилия Имя, группа]

Примечание: в моём репозитории основная ветка называется main (в задании master). Везде, где в задании указан master, я использую main.

Все файлы лежат в папке lab9_git. Скриншоты находятся в папке img.

---

## Начальная настройка

Создан репозиторий на github.com и клонирован на компьютер. В нём создана папка lab9_git с файлом README.md (этот отчёт).

Настроены имя и почта для коммитов:

git config --global user.name "[Имя]"
git config --global user.email "[почта]"
---

## Оценка 3

### Часть 1. Файлы, stage и коммиты

#### 1. На какой ветке я нахожусь (git status)

![git status](img/01_status.png)

Я нахожусь на ветке main. Она совпадает с origin/main на GitHub.

#### 2. Как выглядит git log

![git log](img/02_log.png)

В журнале пока только начальный коммит, созданный GitHub при создании репозитория.

#### 3. Создан файл sort.c

В папке lab9_git создан файл sort.c с функцией сортировки пузырьком (только сама функция, без main).

#### 4. git status после создания файла

![status untracked](img/03_status_untracked.png)

Файл новый, git его ещё не отслеживает. Он находится в разделе Untracked files.

#### 5-6. git add и git status

git add sort.c
![status staged](img/04_status_staged.png)

После git add файл попал в stage (область индексации). Теперь он в разделе Changes to be committed, то есть будет включён в следующий коммит.

#### 7-8. Коммит и git status

git commit -m "Add sort.c"
![status after commit](img/05_status_after_commit.png)

Файл sort.c закоммичен и больше не отображается в списке изменений. Оставшиеся в Untracked файлы (README.md, img/) я ещё не добавлял в git.

#### 9-10. Добавлен комментарий в sort.c, git status

В начало файла добавлен комментарий // моя сортировка.

![status modified](img/06_status_modified.png)

Файл теперь в разделе Changes not staged for commit (modified). Изменение есть в рабочей папке, но в stage оно ещё не добавлено.

#### 11-12. git add и git status

git add sort.c
![status modified staged](img/07_status_modified_staged.png)

Изменение добавлено в stage: файл снова в разделе Changes to be committed (modified).

#### 13-15. Ещё одно изменение, коммит, status и log

Я изменил файл ещё раз (добавил ещё один комментарий) и сделал коммит:

git commit -m "Add comment"
![status after second commit](img/08_status_after.png)

![git log](img/09_log.png)

Коммит сохраняет только то, что было в stage на момент git add. Изменение, сделанное уже после git add, в stage не попало, поэтому его нужно добавлять отдельно. [Опиши, что именно показал твой status: был ли sort.c в modified после коммита или в статусе было чисто.]

#### 16. Добавление в stage и коммит последнего изменения

git add sort.c
git commit -m "Update comment"
[Если коммитить было нечего, напиши: «git сообщил, что коммитить нечего, так как все изменения sort.c уже были закоммичены».]

![git log --oneline](img/10_log_oneline.png)

#### 17. Отправка на удалённый репозиторий

git push
![git push](img/11_push.png)

Коммиты отправлены на GitHub. Файл lab9_git/sort.c появился в репозитории.

![github](img/12_github.png)

---

### Часть 2. Ветки

# Скриншоты работы с ветками

![branch list](img/3/ИМЯ_ФАЙЛА.png)
Список веток.

![status mybranch](img/3/ИМЯ_ФАЙЛА.png)
status на mybranch.

## Оценка 4

### git diff и git diff --staged
![diff](img/4/41_diff.png)
После изменения sort.c git diff показывает добавленные строки, а git diff --staged пуст: в stage ничего нет.

![diff staged](img/4/44_diff_staged.png)
После git add картина обратная: git diff пуст, git diff --staged показывает изменения.

Объяснение. git diff сравнивает рабочую папку со stage, git diff --staged сравнивает stage с последним коммитом. После второго изменения файл существует в трёх состояниях: коммит, stage и рабочая папка, поэтому diff'ы показывают разное, и в git status файл sort.c виден дважды.

### git restore
![restore](img/4/48_status_after_restore.png)
git restore --staged sort.c убрал файл из stage, правки в файле остались.

git restore sort.c отменил незакоммиченную правку (printf), файл вернулся к последнему коммиту.

### Ветки и fast-forward
![ff merge](img/4/ff/ff_06_merge.png)
Ветка feature/uppercase слита в main в режиме fast-forward: main просто передвинулся вперёд, отдельного коммита слияния не создавалось, потому что main не расходился с веткой.

### Слияние mybranch в main
![graph](img/4/ff/ff_10_graph.png)
Ветка mybranch слита в main, на графе видна точка слияния.