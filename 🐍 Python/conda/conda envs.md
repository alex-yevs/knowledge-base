
### ✅ **Создание виртуального окружения**

```bash
conda create --name myenv python=3.10
```

- `myenv` — имя окружения.
- `python=3.10` — версия Python (можно не указывать, тогда будет установлена версия по умолчанию).

**Пример с установкой пакетов сразу:**

```bash
conda create --name myenv python=3.10 numpy pandas
```

---

### ✅ **Активация окружения**

```bash
conda activate myenv
```

---

### ✅ **Деактивация окружения**

```bash
conda deactivate
```

---

### ✅ **Удаление окружения**

```bash
conda remove --name myenv --all
```

- `--all` — удаляет всё, связанное с окружением.

---

### 🔍 **Список всех окружений**

```bash
conda env list
```

или

```bash
conda info --envs
```

