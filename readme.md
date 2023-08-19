#Шпаргаоки по GIT

##Шпаргалка по Markdown

[Щпаргалка](https://gist.github.com/fomvasss/8dd8cd7f88c67a4e3727f9d39224a84c)
[Шпаргалка на истоник](https://www.markdownguide.org/cheat-sheet/)

### Базовые возможности консоли

**Навигация**
pwd (от англ. print working directory, «показать рабочую папку») — покажи, в какой я папке;
ls (от англ. list directory contents, «отобразить содержимое директории») — покажи файлы и папки в текущей папке;
ls -a — покажи также скрытые файлы и папки, названия которых начинаются с символа .;
cd first-project (от англ. change directory, «сменить директорию») — перейди в папку first-project;
cd first-project/html — перейди в папку html, которая находится в папке first-project;
cd .. — перейди на уровень выше, в родительскую папку;
cd ~ — перейди в домашнюю директорию (/Users/Username);
cd / — перейди в корневую директорию.


**Работа с файлами и папками**
**Создание**
touch index.html (англ. touch, «коснуться») — создай файл index.html в текущей папке;
touch index.html style.css script.js — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;
mkdir second-project (от англ. make directory, «создать директорию») — создай папку с именем second-project в текущей папке.
**Копирование и перемещение**
cp file.txt ~/my-dir (от англ. copy, «копировать») — скопируй файл в другое место;
mv file.txt ~/my-dir (от англ. move, «переместить») — перемести файл или папку в другое место.
**Чтение**
cat file.txt (от англ. concatenate and print, «объединить и распечатать») — распечатай содержимое текстового файла file.txt.
**Удаление**
rm about.html (от англ. remove, «удалить») — удали файл about.html;
rmdir images (от англ. remove directory, «удалить директорию») — удали папку images;
rm -r second-project (от англ. remove, «удалить» + recursive, «рекурсивный») — удали папку second-project и всё, что она содержит.

---

### Работа с GIT

git init # создали репозиторий 

rm -rf .git # удалили подпапку .git 
**Проверить состояние репозитория** — git status

git add --all # подготовили к сохранению все файлы в репозитории
git add todo.txt
git add todo.txt

**Сделать коммит**

git commit -m ‘Мой первый коммит!’ 


**Просмотреть историю коммитов** — git log

##Создание глобального репозитория

Сначала создается репозиторий через NEW, название может быть любое и необязательно совпадать с локальным


# Связываем локальный и удаленный репозиторий

**Привязать удалённый репозиторий к локальному** — git remote add

Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.

Откройте консоль, перейдите в каталог локального репозитория и введите команду git remote add

``` Bash
$ cd ~/dev/first-project
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```
Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.
origin (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

Убедиться, что репозитории связаны, — git remote -v

##Синхронизируем локальный и удалённый репозитории

**Отправить изменения на удалённый репозиторий ** — git push


echo "# git-notes" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Sipalex/git-notes.git
git push -u origin main

git remote add origin git@github.com:Sipalex/git-notes.git
git branch -M main
git push -u origin main


## РАбота с  SSH

$ ls -la .ssh/ # вывели список созданных ключей 

Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
    Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.
    Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования ed25519. Ничего страшного: используйте другой алгоритм.
$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
    После ввода отобразится такое сообщение.
> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 
Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите Enter.
macOS
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter] 
         Windows
> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter] 
    Теперь в указанной директории появится пара ключей.
Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите Enter, а затем ещё раз Enter для подтверждения.
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again] 
💡 Быть или не быть кодовой фразе — вот в чём вопрос
Как бы странно ни звучало, кодовая фраза — это «пароль от ключа». Представьте, что SSH-ключ лежит в шкатулке. А на самой шкатулке — кодовый замок, который открывается кодовой фразой.
Многие пользователи Git не используют кодовую фразу для защиты своего SSH-ключа. Если такой фразы нет, то её не нужно вводить всякий раз при взаимодействии с удалённым репозиторием.
С другой стороны, применение кодовой фразы усиливает безопасность ключей. Если вы используете эту фразу, ключ будет надёжно защищён в случае несанкционированного доступа к вашему компьютеру.
Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.
ls -a ~/.ssh 
    На экране должны появиться два файла — один с расширением .pub, другой — без. Файл в .pub — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения .pub — приватный. Ни в коем случае не передавайте его никому! 
    Вся последовательность действий в консоли показана на скриншоте ниже.
	
	
	
	
	Привязываем SSH-ключ к GitHub
В прошлом уроке вы сгенерировали SSH-ключ, но он пока не привязан к аккаунту на GitHub. Исправим это.
Инструкция по связыванию SSH-ключа и GitHub-аккаунта
После выполнения команды ssh-keygen из предыдущего урока в директории ~/.ssh будет создано два файла — id_ed25519 и id_ed25519.pub (или id_rsa и id_rsa.pub — в зависимости от того, какой алгоритм вы использовали):
id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
Скопируйте содержимое файла с публичным ключом в буфер обмена.
macOS
# скопировать содержимое ключа в буфер обмена:
$ pbcopy < ~/.ssh/id_rsa.pub
# для ed25519:
$ pbcopy < ~/.ssh/id_ed25519.pub 
Здесь используется команда pbcopy — она копирует поток данных в буфер обмена. Запись pbcopy < ~/.ssh/id_rsa.pub означает: «Скопируй в буфер обмена всё содержимое файла ~/.ssh/id_rsa.pub».
В качестве альтернативы вы можете распечатать файл на экран с помощью cat ~/.ssh/id_rsa.pub и скопировать его вручную.
Windows
# скопировать содержимое ключа в буфер обмена:
$ clip < ~/.ssh/id_rsa.pub
# для ed25519:
$ clip < ~/.ssh/id_ed25519.pub 
Если clip не сработает, выведите содержимое файла с помощью cat ~/.ssh/id_rsa.pub или cat ~/.ssh/id_ed25519.pub и скопируйте вывод в буфер обмена из консоли.
Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.

В меню слева нажмите на пункт SSH and GPG keys.

В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).

В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).
В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).
В поле Key скопируйте ваш ключ из буфера обмена.


8. Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).

Проверьте правильность ключа с помощью следующей команды.
$ ssh -T git@github.com 
Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub по этой ссылке. Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите yes, чтобы продолжить. Вы увидите приветствие на экране.
Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access. 
Если у вас возникли сложности при генерации или привязке SSH-ключей, посмотрите видеоинструкцию, в которой мы показываем всё по порядку.


#Git log, Хэш. Head
Получить сокращённый лог — git log --oneline
Получить сокращённый лог можно с помощью команды git log с флагом --oneline (англ. «одной строкой»). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.



```mermaid
$ pwd # посмотрели, где мы
/Users/user/dev/first-project

$ cd .git/
$ ls # посмотрели, какие есть файлы
COMMIT_EDITMSG  ORIG_HEAD  description  index  logs/     refs/
HEAD            config     hooks/       info/  objects/

$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка
```


Внутри HEAD — ссылка на служебный файл: refs/heads/master (или refs/heads/main в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.В числе прочих файлов в папке .git есть служебный файл HEAD. Он указывает на самый свежий коммит.
Вместо хеша последнего коммита можно написать слово HEAD — Git вас поймёт.

#Статусы файлов в Git
Статусом untracked помечается файл, о существовании которого Git знает, но не следит за изменениями в нём. Этот статус — противоположность tracked, в который попадают все файлы, отслеживаемые Git.
Файл переходит в статус staged после выполнения git add.
Статус modified означает, что файл был изменён.
Большинство файлов в проектах «шагает» по следующему циклу: «изменён» → «добавлен в список на коммит» → «закоммичен» → «изменён» → и так далее.

*Как читать git status*
Особое внимание уделите материалу о статусах и жизненном цикле файлов в Git. Схему изменения статусов можно описать словами. Например, modified+git add = staged.
Команда git status всегда подскажет, что происходит с файлом: например, он добавлен в список «на коммит» или ещё вообще не отслеживается, или изменён.
git status показывает явно следующие состояния файлов: untracked, staged и modified.
git status подсказывает, какие команды можно выполнить, чтобы поменять состояние файла.


*Правильно описывать коммиты *— искусство, к которому стоит приобщиться как можно раньше. Хорошо, когда:
сообщение коммита легко читается;
оно информативное;
все сообщения оформлены в одном стиле.
💡 Инфинитив и императив
Для сообщений на русском языке часто рекомендуют использовать инфинитивы. Например: Добавить тесты для PipkaService, Исправить ошибку #123 и так далее.
Для сообщений на английском рекомендуется использовать повелительное наклонение (англ. imperative). Например: Use library mega_lib_300, Fix exit button и так далее.

```mermaid
graph LR;
  untracked -- "git add" --> staged;
  staged    -- "???"     --> tracked/comitted;

%% стрелка без текста для примера: 
  A --> B;
``` 