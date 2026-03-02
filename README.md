# Подготовка к собесам по Git

<img width="699" height="746" alt="image" src="https://github.com/user-attachments/assets/58414998-47c6-4d5e-82c0-8236f39360a7" />

Вот что касается теории по данному инструменту 

<img width="507" height="156" alt="image" src="https://github.com/user-attachments/assets/be743153-1915-489a-9d81-2d519ccaadf4" />

Ветка - отдельная линия разработки 

```
A — B — C  (main)
         \
          D — E (feature)
```
commit - snapshot файлов 
branch - ссылка на коммит 
HEAD - указатель на текущую ветку

Что такое Теги tags?

<img width="609" height="187" alt="image" src="https://github.com/user-attachments/assets/5cf96d4e-4f3b-4d47-b3b1-1b17ba56f92d" />

По сути, теги - это просто фиксированная ссылка на конкретный коммит 

<img width="621" height="194" alt="image" src="https://github.com/user-attachments/assets/5b15ea6f-93a1-4d0d-b203-d7df2eb84856" />

Вот разницу тэгов и веток

<img width="240" height="247" alt="image" src="https://github.com/user-attachments/assets/7493fb91-3b4b-4bdb-ba66-9bbac031aa1a" />

Markdown - это по сути просто формат файлов, обычно используется для документации 

## Основные команды для работы с git

```
git init - инициализация локального git репо 
git add . - добавляем файлы в индекс
git commit -m "name" - создаем коммит из индекса, snapshot текущего состояния
git push - пушим код в репо удаленный
git pull - посмотреть изменения и скачать их себе локально, объединив с нашими изменениями, чтобы не было конфликтов
git switch - переключение между ветками
git rebase - переписывание истории, стори становится более чистой, но если кто то еще работает по этой ветке, то у него просто история слетит
git merge - то же самое что и rebase, только он не переписывает историю, а создает новый merge коммит
git fetch - проверить, есть ли изменения у нас в репо удаленном, но не применять их локально 
git diff - показывает разницу 
git revert - мы можем создать новый коммит на основе того, на который хотим откатиться
git reset (--soft --mixed--hard) - это переписывание истории, то есть мы тут прям откатываемся на нужный коммит, и переписываем историю
```

## Какие стратегии ветвления бывают?
Git flow
у нас есть разные ветки, одна main, другая для фич, еще одна для разрабов и так можно создать кучу разных веток для своих задач

Trunk-Based development 
одна main ветка, маленькие частые коммиты, современный подход

GitHub flow 
это самый простой, main, feature, PR, merge

## Вопросы для собесов

<img width="545" height="358" alt="image" src="https://github.com/user-attachments/assets/932bed26-9254-487b-9065-4b44b6a9f75f" />

Вот такие вопросы на собесах про Git бывают

1. Как перенести коммиты из одной ветки в другую?
Можно использовать для этой задачи git cherry-pick hash
Сначала переключусь на нужную мне ветку, выполню команду, выберу например один или диапазон коммитов, далее просто перенесем его на нужную ветку

<img width="985" height="434" alt="image" src="https://github.com/user-attachments/assets/b39a19a6-82a6-4d42-8a6b-6b98cf450fd1" />

Создадим репо на гитхабе например

<img width="407" height="222" alt="image" src="https://github.com/user-attachments/assets/248a86f9-b25b-4ec6-8d97-441c4bef9f92" />

Создадим новую ветку и переключимся на нее 

```
git log --oneline --graph --decorate --all
```
Вот такой командой можно посмотреть дерево версий Git

```
 git switch main
```
Переключимся на нужную ветку

```
git cherry-pick 25ae507
```
Выполним команду cherry-pick и hash коммита берем

<img width="429" height="101" alt="image" src="https://github.com/user-attachments/assets/8e06b27e-5ecd-47f5-8bea-1d7dd4195850" />

Проверяем дерево, у нас создался новый коммит в main ветке с другим hash

Второй способ - это merge, просто сделать merge ветки feature в ветку main, и изменения у нас применятся 

Третий способ - это сделать git rebase, это переписывание истории коммитов на нашей ветке, то есть у нас новая ветка аля всегда изменялась поверх новой версии main ветки 

### Что такое merge conflict и почему возникает?

<img width="521" height="72" alt="image" src="https://github.com/user-attachments/assets/511fe938-2944-42f3-987f-2c15e6e0ee12" />

Merge confilct - это ситуация, когда Git не смог применить изменения, которые мы тут понаписали

<img width="607" height="355" alt="image" src="https://github.com/user-attachments/assets/5f316649-783c-4804-bbab-6ed8f7e994e7" />

Самый просто вариант, это когда у нас в один и тот же участок кода вносились изменения в разных ветках, и Git не понимает какое именно изменение надо применить 

<img width="619" height="223" alt="image" src="https://github.com/user-attachments/assets/60871136-1241-4211-b96e-4a3e1b9fb828" />

Вот так это нам Git подсветит в коде

<img width="222" height="157" alt="image" src="https://github.com/user-attachments/assets/fb0d3a36-5fa1-4c4b-804a-435ddb1fc7ba" />

Как это фиксить?
Надо открыть конфликтный файл, удалить маркеры и оставить только нужную нам строку
далее сделать git add и git commit и вуаля, наш merge conflict решен успешно 

<img width="485" height="95" alt="image" src="https://github.com/user-attachments/assets/96942e84-4ee9-4456-a2de-64a205b9dfe1" />

Вот так у нас выглядит конфликт 

<img width="210" height="95" alt="image" src="https://github.com/user-attachments/assets/55905d3f-c5ad-465a-98cc-7a298bda0f7d" />

Мы убрали лишний мусор и оставили только вот нужный нам код

Конфликт может возникать не только при merge, но и при rebase тоже

### Как работает Git pull под капотом?

git pull = git fetch + git merge

<img width="362" height="248" alt="image" src="https://github.com/user-attachments/assets/293b3018-8131-4584-8e23-f90716837598" />

Это по сути проверка нашего репозитория на изменения, и их же применение, то есть будет создаваться у нас новый коммит при git merge

<img width="632" height="193" alt="image" src="https://github.com/user-attachments/assets/3d6aefa1-a2a0-435f-86c6-079e3a97f61c" />

еще можно сделать вот так, чтобы у нас не было лишних конфликтов, через git pull origin main --rebase

<img width="636" height="121" alt="image" src="https://github.com/user-attachments/assets/d36d4344-4af7-45c2-a2e9-2538b7a36a2e" />

Git pull - это комбинация git fetch и git merge, сначала у нас скачиваются изменения в remote tracking branch, затем происходит merge в текущую ветку

## Чего то новое, что не было в roadmap, интересные кейсы

Вот и все что касается теории и практики по гиту, основной workflow - это git clone, либо git pull, далее работаем с кодом, добавляем изменения в index через git add ., потом создаем коммиты из этих индексов, и можем пушить в репозиторий, так же создавать PR/MR на наших WEB UI, ждать пока нам сделают code review, и уже потом пропустят либо не пропустят код дальше, вот и в принципе весь workflow с Git у DevOps'ов
