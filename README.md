# Git commands
---

### Отменяет не-закоммиченные изменения в указанном файле, возвращая его к состоянию последнего коммита
- `git checkout .` — отменяет все незакоммиченные и не индексированные изменения во всех файлах.
- `git restore <путь_к_файлу>` — в указанном файле.
- `git restore --staged <имя файла>` — удаляет файл из индекса (после git add)

---

### Показывает разницу между файлами.  
Не-закоммиченные изменения в рабочей директории.  
Если добавить флаг (например, `git diff HEAD`), покажет разницу между текущими изменениями и указанным коммитом.  
Полезно для анализа, что было изменено перед коммитом.
```
git diff
```

---

### Сохраняет изменения в рабочем дереве (не-закоммиченные изменения и индексированные файлы) во временное хранилище (stash) и очищает рабочую директорию
Используется, чтобы переключиться на другую ветку без коммита текущих изменений.
```
git stash
```
Чтобы удалить изменения, сохраненные в git stash, можно воспользоваться следующими командами:
1) Удалить самый последний сохраненный слой изменений:
```
git stash drop
```
Эта команда удалит самый последний stash. Если вы хотите удалить конкретный stash, нужно указать его идентификатор, например:
```
git stash drop stash@{0}
```
2) Удалить все сохраненные слои изменений:
```
git stash clear
```
Эта команда удалит все записи в stash, включая все сохраненные изменения.

3) Вывод списка stash. Если вы хотите увидеть список всех сохраненных stash, вы можете использовать команду:
```
git stash list
```
После этого вы сможете увидеть идентификаторы stash и выбрать, какой из них удалить.

---

### Показывает текущее состояние репозитория 
- Какие файлы изменены, добавлены, удалены или не отслеживаются.  
- Какие файлы готовы к коммиту.  
- На какой ветке вы находитесь.  
- Есть ли несохраненные изменения.
```
git status
```

---

### История коммитов 
- `--oneline` — компактный вывод  
- `--graph` — визуализация веток  
- `--pretty=format:"%h - %an, %ar : %s"` — кастомный формат вывода
- `--oneline -n 3` — Последние N коммитов
```
git log
```

---

### Создает коммит из подготовленных изменений  
- `-m "message"` — добавить сообщение коммита  
- `--amend` — заменяет последний коммит новым: открывает редактор для изменения сообщения, также включает новые проиндексированные файлы (если есть).	
- `--no-edit` — использовать предыдущее сообщение коммита
- `--amend -m "новое сообщение"` — заменяет последний коммит новым: можно изменить сообщение и добавить новые проиндексированные файлы, не открывая редактор.
```
git commit
```

---

### Команда объединяет изменения из указанной ветки в ту ветку, на которой вы сейчас находитесь  

Допустим, у вас есть две ветки: `master` и `feature`.  
Вы работаете в ветке `feature`, делаете изменения и коммиты.  
Когда изменения готовы, переключаетесь на ветку `master`,  
Затем объединяете ветку `feature` с `master`:
```
git merge feature
```
В результате все изменения из ветки `feature` окажутся в ветке `master`.  
Если Git может объединить изменения автоматически, он сделает это,  
а если возникают конфликты, вам нужно будет их решить вручную.

```
git merge [branch]
```

---

### Копирует отдельный коммит (с указанным хешем) из другой ветки и применяет его к текущей  
То есть, изменения этого коммита «переносятся» в вашу ветку, создавая новый коммит с таким же содержимым, но новым идентификатором.
```
git cherry-pick [commit]
```

---

### Управление удаленными репозиториями
```
git remote
```
- `-v` — показать URL удаленных репозиториев  
- `set-url [name] [url]` — изменить URL репозитория  
- `add [name] [url]` — добавить новый удаленный репозиторий

---

### Работа с большими файлами в Git
```
git lfs
```

---

### Настройка конфигурации Git
```
git config
```

---

### Показывает кто и когда менял каждую строку файла
```
git blame
```

---

### Помогает найти коммит, внесший баг через бинарный поиск
```
git bisect
```

---

### Создает тег для текущего коммита (`git checkout имя_тега`)
```
git tag [name]
```

---

### Временно сохраняет незакоммиченные изменения  
- `apply` — Применяет изменения из stash (по умолчанию — последний). Не удаляет их из списка stash'ей. Повторно использовать можно. То есть, ты можешь применить одни и те же изменения несколько раз (например, на разных ветках или при неудачной попытке применения).
- `pop` — Применяет изменения, как apply. И удаляет их из списка stash'ей (удаляет последний по умолчанию). Одноразово, применил — и исчез.
```
git stash
```

---

### Показывает историю изменений HEAD
```
git reflog
```

---

### Если во время разработки содержимое ветки в удаленном репозитории изменилось  
И если нужно забрать изменения себе в локальную ветку.  
Если я делал ответвление от `main` и она обновилась, и этой обновы нету в моей фича-ветке:
```
git pull --rebase origin main
```
- Забирает последние изменения из main с удалённого репозитория.
- "Приклеивает" (rebase) твои коммиты поверх этих изменений, как будто ты начал работать от актуального main.
- Чистая история - 	Rebase делает историю линейной, без merge-коммитов. Удобнее читать, разбираться и ревьювить.
- В main могли появиться важные фиксы, без них ты рискуешь работать на устаревшей базе.

🚨 Важно:
Если ты уже запушил свою ветку в удалённый репозиторий, и потом сделал rebase, то тебе придётся делать:
```
git push --force
```
Потому что коммиты после rebase — это уже другие коммиты (с другими ID).

---

### Показывает, как выглядел файл в конкретном коммите
```
git show <хеш_коммита>:<имя_файла>
```

---

### Быстрый коммит
Коммитит изменённые и отслеживаемые файлы (те, что уже были в Git).
Новые файлы не добавляет.
Удобно, если просто правил существующий код.

- Только изменил старые файлы `git commit -am "..."`
- Есть новые файлы `git add . + git commit -m "..."`
```
git commit -am "сообщение"
```

---

### Полностью удалить последний коммит вместе с изменениями
Удаляет последний коммит текущей ветки и откатывает изменения из него (всё исчезнет: и из истории, и из файлов).

Никакого нового коммита не создаёт, просто «отматывает» ветку назад.

Подходит, если нужно полностью отменить последний коммит и всё, что в нём было.
```
git reset --hard HEAD~1
```

Вернуть коммит в состояние "проиндексировано" (staged).
Откатывает последний коммит, но оставляет изменения в индексе (staging area), как будто ты только что сделал git add.
Полезно, если ты хочешь переделать коммит или изменить сообщение.
```
git reset --soft HEAD~1
```
- Коммит удаляется из истории.
- Изменения остаются в индексе.
- Можно сразу снова коммитить (или внести правки и закоммитить).

---

### Отмена последних N коммитов без удаления (revert)
Создаёт новый коммит, который отменяет изменения из предыдущих коммитов (не удаляет их из истории).

В отличие от git reset, этот метод не изменяет историю и подходит для работы с публичными ветками.


- `git revert -n` — отменяет изменения без создания коммита сразу. Ты получаешь изменения в рабочей директории, которые нужно добавить и закоммитить.
```
git revert -n HEAD~3..HEAD
```

```
git add .
```

```
git commit -m "Starting over from the plot twist."
```

---

### Заменить файл из другой ветки, не переключая её
Заменяет указанный файл в рабочей директории версией этого файла из указанной ветки, не переключая текущую ветку.

Еще одно объяснение:

Вытаскивает конкретный файл из указанной ветки в твою текущую рабочую область. То есть ты остаешься в своей ветке, но файл берется из другой.

Используется, когда нужно получить изменения из другой ветки без переключения на неё.

- имя_ветки — это ветка, из которой ты хочешь взять файл.
- путь_к_файлу — путь к файлу, который нужно заменить.
- Эта команда не коммитит изменения. Если нужно сохранить изменения, после выполнения команды нужно сделать git add и git commit.
- Модификация только файла: Это заменит только указанный файл, не изменяя других файлов в рабочей директории.

```
git checkout имя_ветки -- путь_к_файлу
```

---

### Возврат конкретного файла к предыдущему состоянию
Если нужно откатить только один файл к версии из старого коммита, можно использовать эти команды.
- `git show <хеш_коммита>:<имя_файла>` — показывает содержимое файла из конкретного коммита. Ты можешь увидеть, как файл выглядел на момент этого коммита.
- `git checkout <хеш_коммита> -- <имя_файла>` — возвращает файл в рабочую директорию в том виде, как он был в указанном коммите (не переключая ветку).

Команда `git checkout` не изменяет историю коммитов, а просто обновляет файл в рабочей директории.
Если хочешь сохранить изменения, нужно сделать `git add` и `git commit`.

Посмотреть содержимое файла на момент коммита:

```
git show <хеш_коммита>:<имя_файла>
```

Вернуть файл к этой версии:
```
git checkout <хеш_коммита> -- <имя_файла>
```

---

### Восстановление файла из другой ветки без изменения staging
Восстанавливает файл из указанного источника, не затрагивая изменения в staging (индекс), пока ты явно не добавишь файл в индекс.

По умолчанию восстанавливает файл из последнего коммита текущей ветки, но с помощью параметра `--source` можно указать другой источник, например, другую ветку.
- `--source=ветка` — указывает ветку, из которой нужно восстановить файл.
- `путь_к_файлу` — путь к файлу, который ты хочешь восстановить.
- `git restore` — это более новая команда, которая заменяет старый git checkout для работы с файлами, и она не затрагивает staging (индекс) до тех пор, пока ты явно не добавишь файл.

В отличие от `git checkout`, `git restore` не добавляет файл в индекс автоматически, поэтому ты можешь сначала увидеть изменения в рабочей директории и только потом решить, что с ними делать.

Восстановить файл из другой ветки:
```
git restore --source=ветка путь_к_файлу
```

---

### Применить конкретный коммит из другой ветки
Позволяет взять конкретный коммит из другой ветки и применить его в текущей ветке. Это полезно, если нужно не просто взять последнюю версию файла, а именно конкретное изменение с его историей.

- `git cherry-pick <хеш_коммита>` — применяет изменения из указанного коммита и создает новый коммит в текущей ветке.
- `git cherry-pick -n <хеш_коммита>` — применяет изменения из коммита в рабочую директорию и staging area, но не создает коммит. Это полезно, если ты хочешь внести изменения, но ещё не готов к коммиту, или хочешь немного подправить их перед фиксацией.
- Создаётся новый коммит: даже если изменения из другого коммита, создаётся новый коммит в текущей ветке с новым хешем.
- Конфликты: как и при обычном слиянии, если изменения в коммите конфликтуют с текущими изменениями, нужно будет разрешить конфликты вручную.
- Staging area — это область, где ты подготавливаешь изменения для следующего коммита. Они попадают туда с помощью команды git add. Эти изменения ещё не зафиксированы в истории репозитория.

Применить коммит и создать новый коммит в текущей ветке:
```
git cherry-pick <хеш_коммита>
```

Добавить изменения из коммита в staging area без создания коммита (это позволяет дальше редактировать изменения перед коммитом):
```
git cherry-pick -n <хеш_коммита>
```
