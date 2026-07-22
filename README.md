# Домашнее задание к занятию «Инструменты Git» Губайдуллин Андрей

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?
* Сколько родителей у коммита `b8d720`? Напишите их хеши.
* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.
* Кто автор функции `synchronizedWriters`? 

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

---

### Ответ

*1. Полный хеш и комментарий коммита, хеш которого начинается на aefea:
   <img width="487" height="110" alt="image" src="https://github.com/user-attachments/assets/729d914d-1e7d-420b-b50d-037c8a6cb7bb" />
   
Полный хеш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545

Комментарий: Update CHANGELOG.md

Как получчили:
Для поиска коммита используется команду git show:


git show aefea --pretty=format:'Hash = %H %nComment: %s' -q

--pretty=format:... задает нужный формат вывода (%H — полный хеш, %s — комментарий)

-q (сокращение от --no-patch) подавляет вывод информации о изменениях в файлах

*2. Какому тегу соответствует коммит 85024d3?

Ответ:
Коммит 85024d3 соответствует тегу v0.12.23.

Как получили:
Информацию мможно получить с помощью git show или git log:
<img width="489" height="52" alt="image" src="https://github.com/user-attachments/assets/a91a2955-da3d-444b-a032-f38a7cb90fa3" />
git show 85024d3 --oneline -q
--oneline сокращает вывод до одной строки, где в скобках отображаются все ссылки (ветки и теги), указывающие на этот коммит.

В выводе команды присутствует tag: v0.12.23

*3. Сколько родителей у коммита b8d720? Напишите их хеши.

У коммита b8d720 два родителя

Хеш первого родителя: 56cd7859e (полный: 56cd7859e05c36c06b56d013b55a252d0bb7e158)

Хеш второго родителя: 9ea88f22f (полный: 9ea88f22fc6269854151c571162c5bcf958bee2b)

Как получили:
Определим через git show:
<img width="519" height="122" alt="image" src="https://github.com/user-attachments/assets/c5a6cbbd-325f-4abf-a574-cfbf7b75eccd" />

git show --source b8d720 --pretty=short
В выводе есть строка Merge: 56cd7859e 9ea88f22f, которая указывает на два родительских коммита

4. Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.

Между тегами v0.12.23 и v0.12.24 были сделаны коммиты:

Хеш и	комментарий
33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24) v0.12.24
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release

Как получили:
Для получения списка используем команду git log с указанием диапазона:

<img width="765" height="189" alt="image" src="https://github.com/user-attachments/assets/00074415-2916-4dc1-bc57-508e537ce969" />

git log v0.12.23..v0.12.24 --pretty=oneline
v0.12.23..v0.12.24 — стандартная запись диапазона в Git, означающая "все коммиты, достижимые из v0.12.24, но не достижимые из v0.12.23".

--pretty=oneline выводит каждый комммит в одну строку показывая полный хеш и комментарий

Чтобы исключить сам коммит v0.12.24, можно использовать v0.12.23..v0.12.24^.

5. Найдите коммит, в котором была создана функция func providerSource

Функция func providerSource была создана в коммите:

Хеш (сокращенный): 8c928e8358

Хеш (полный): 8c928e83589d90a031f811fae52a81be7153e82f

Как получили:
Для поиска коммита, используется опция -S (pickaxe) команды git log:

<img width="572" height="58" alt="image" src="https://github.com/user-attachments/assets/fe73e001-3e8a-45fe-9a44-c754ccf05601" />

git log -S 'func providerSource(' --oneline
-S ищет коммиты, в которых количество вхождений указанной строки изменилось.

Первый (самый старый) коммит в выдаче будет тем, где функция была создана.

6. Найдите все коммиты, в которых была изменена функция globalPluginDirs

Найти файл, содержащий определение функции:

<img width="605" height="211" alt="image" src="https://github.com/user-attachments/assets/8604c217-4b44-47d4-a7ad-10afc736306e" />

Список коммитов 
Хеш	Комментарий
7c4aeac5f3	stacks: load credentials from config file on startup (#35952)
65c4ba7363	Remove terraform binary
125eb51dc4	Remove accidentally-committed binary
22c12df86	Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a	Don't show data while input if sensitive
35a058f3d	main: configure credentials from the CLI config file
c0b1761096	prevent log output during init
8364383c35	Push plugin discovery down into command package

Как получили: 

git log -S"globalPluginDirs" --oneline

Команда находит все коммиты, в которых количество вхождений строки globalPluginDirs


7. Кто автор функции synchronizedWriters?
Команда
 git log -S"func synchronizedWriters(" --pretty="%h %an %ad" --reverse

автор функции synchronizedWriters - Martin Atkins
<img width="536" height="78" alt="image" src="https://github.com/user-attachments/assets/219e3ca7-0c58-49c3-b117-c54794d97da9" />

Как получили:
Для поиска первого упоминания функции используется команда git log с опцией -S:

git log -S"func synchronizedWriters(" --pretty="%h %an %ad" --reverse
-S ищет коммиты где менялось количество вхождений строки.

--reverse выводит коммиты в хронологическом порядке (сначала самые старые).

--pretty="%h %an %ad" выводит хеш, имя автора и дату.

Самый первый коммит указывает на автора.


