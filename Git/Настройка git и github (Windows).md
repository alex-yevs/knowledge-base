## ✅ Что уже есть:

- Git настроен на Ubuntu
- SSH-ключ сгенерирован (`~/.ssh/id_ed25519` и `.pub`)
- Этот ключ уже добавлен в GitHub
___
## 🧩 Цель:

- Установить Git на Windows
- Перенести SSH-ключ с Ubuntu
- Подключиться к GitHub через SSH
- Проверить и начать работу
___
## 🪟 Шаг 1: Установка Git на Windows

1. Скачай Git с официального сайта: [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. Установи Git. В процессе установки:
    - Оставляй настройки по умолчанию
    - Убедись, что выбран SSH-клиент **"Use bundled OpenSSH"**
3. После установки - открой **Git Bash** (идёт в комплекте)
___
## 📁 Шаг 2: Перенос SSH-ключа с Ubuntu

#### На Ubuntu:
```bash
scp ~/.ssh/id_ed25519* user@windows-pc:/путь/куда/положить
```

Или скопируй вручную файлы:
- `~/.ssh/id_ed25519`
- `~/.ssh/id_ed25519.pub`

#### На Windows:

1. Создай папку `.ssh` в своём домашнем каталоге, если её нет:
```bash
mkdir ~/.ssh
```

2. Перенеси оба файла туда: `id_ed25519` и `id_ed25519.pub`

3. Проверь права (важно!):
```bash
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```
___
## 🧠 Шаг 3: Добавление ключа в ssh-agent

Запусти ssh-agent:
```bash
eval "$(ssh-agent -s)"
```

Добавь ключ:
```bash
ssh-add ~/.ssh/id_ed25519
```
___
## 🧪 Шаг 4: Проверка подключения к GitHub

В Git Bash:
```bash
ssh -T git@github.com
```
Если всё настроено - увидишь:
> Hi your_username! You've successfully authenticated…
___
## 🛠 Шаг 5: Настройка Git на Windows

Если ещё не делал:
```bash
git config --global user.name "Твоё имя"
git config --global user.email "youremail@example.com"

git config --global core.quotepath false
```
___
## 🔗 Шаг 6: Клонирование репозитория с GitHub (через SSH)
```bash
git clone git@github.com:твоя_учетка/имя_репозитория.git
```
___
