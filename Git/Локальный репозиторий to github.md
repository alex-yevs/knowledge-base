#### **1. Создай репозиторий на GitHub**

- Зайди на [github.com](https://github.com).
- Нажми кнопку **"New"** (или "+" → New repository).
- Укажи имя репозитория (например, `my-project`), описание — по желанию.
- Не создавай `README`, `.gitignore` или license — потому что они уже могут быть у тебя локально.
- Нажми **Create repository**.
---
#### **2. В терминале, в папке с твоим проектом:**

Если в папке **уже инициализирован git** (у тебя есть `.git` внутри):
```bash
git remote add origin https://github.com/username/my-project.git
git branch -M main  # если ветка называется master, можно её переименовать 
git push -u origin main`
```
> 🔁 Заменить `username` и `my-project` на свои реальные значения.
---

Если **git ещё не инициализирован**, сначала выполни:
```bash
git init
git add .
git commit -m "описание коммита"
```

А потом продолжай:
```bash
git remote add origin https://github.com/username/my-project.git
git branch -M main
git push -u origin main
```
---
#### ✅ Готово!

Теперь твой локальный проект залит на GitHub, и ты можешь дальше пушить изменения обычным способом:
```bash
git add .
git commit -m "какой-то коммит"
git push
```