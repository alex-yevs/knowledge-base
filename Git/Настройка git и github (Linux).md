## 1. Установка Git

Открой терминал и выполни команду:
```bash
sudo apt update
sudo apt install git
```
Проверь установку:
```bash
git --version
```
___
## 2. Настройка имени и почты

Это нужно для подписи коммитов:
```bash
git config --global user.name "<name surname>"
git config --global user.email "<email>"

git config --global core.quotepath false
```

`git config --global core.quotepath` управляет тем, как Git отображает имена файлов, содержащие не-ASCII символы (например, кириллицу, китайские иероглифы, спецсимволы и т. д.) в выводе команд, таких как `git status`, `git diff`, `git log` и др.

- `core.quotepath = true` (по умолчанию): Git будет **экранировать не-ASCII символы** в путях файлов с помощью escape-последовательностей. Например:
 ```console black:1
 docs/\320\241\320\276\321\205\321\200\320\260\320\275\320\270\321\202.txt
 ```
   
- `core.quotepath = false`: Git будет **показывать имена файлов в обычной форме**, если терминал поддерживает нужную кодировку (обычно UTF-8):
```console black:1
docs/Сохранить.txt
```
Проверить настройки можно так:
```bash
git config --list
```
___
## 3. Создание SSH-ключа для GitHub

Чтобы не вводить логин и пароль каждый раз, лучше использовать SSH.
#### Проверить, есть ли уже ключи:
```bash
ls ~/.ssh
```

#### Если ключей нет, создать новый:
```bash
ssh-keygen -t ed25519 -C "youremail@example.com"
```
Нажимай Enter везде, можно оставить путь по умолчанию.
___
## 4. Добавление SSH-ключа в ssh-agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```
>🔄 `ssh-agent` - это своего рода "менеджер ключей". Он: запускается в фоне, хранит приватный ключ (в оперативке), позволяет использовать ключ без постоянного ввода пароля, даёт git доступ к ключу, когда ты пушишь или клонируешь по SSH.
___
## 5. Добавление SSH-ключа в GitHub
```bash
cat ~/.ssh/id_ed25519.pub
```
Скопируй результат.
#### Далее:
1. Перейди на [https://github.com](https://github.com)
2. В правом верхнем углу → твой аватар → **Settings**
3. Слева **SSH and GPG keys** → кнопка **New SSH key**
4. Вставь туда ключ и дай ему имя (например, "Ubuntu Laptop")
___
## ✅ Проверка подключения

Можно выполнить:
```bash
ssh -T git@github.com
```
Если всё ок, будет сообщение:
> Hi your_username! You've successfully authenticated, but GitHub does not provide shell access.
___
