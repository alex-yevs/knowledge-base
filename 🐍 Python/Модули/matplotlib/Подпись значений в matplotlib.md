## 🧰 Основной инструмент — `plt.text()` и `ax.text()`

### Сигнатура:

```python
ax.text(x, y, s, **kwargs)
```

- `x`, `y` — координаты текста;
- `s` — сам текст (строка);
- `**kwargs` — параметры форматирования (цвет, размер, выравнивание и т.п.).

---

## 1️⃣ Линейный график (Line Plot)

### ✅ Задача:

Добавить подписи рядом с каждой точкой линии.

### 🔢 Пример:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 1, 4]

fig, ax = plt.subplots()
ax.plot(x, y, marker='o')

# Добавление подписей к точкам
for i in range(len(x)):
    ax.text(x[i], y[i] + 0.1, f'{y[i]}', ha='center', va='bottom')

ax.set_title("Линейный график с подписями")
plt.show()
```

### 💬 Комментарий:

- `+ 0.1` при `y[i]` — небольшой вертикальный сдвиг, чтобы подпись не накладывалась на точку.
- `ha='center'` — горизонтальное выравнивание текста по центру.

---

## 2️⃣ Столбчатая диаграмма (Bar Chart)

### ✅ Задача:

Отобразить значения над столбцами.

### 🔢 Пример:

```python
import matplotlib.pyplot as plt

labels = ['A', 'B', 'C', 'D']
values = [10, 24, 36, 18]

fig, ax = plt.subplots()
bars = ax.bar(labels, values, color='skyblue')

# Добавление подписей
for bar in bars:
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2, height + 0.5, f'{height}', 
            ha='center', va='bottom')

ax.set_title("Столбчатая диаграмма с подписями")
plt.show()
```

### 💬 Комментарий:

- `bar.get_x() + bar.get_width()/2` — центр столбца.
- `height + 0.5` — небольшое смещение вверх.
- Метод `get_height()` используется для получения значения столбца.

---

## 3️⃣ Круговая диаграмма (Pie Chart)

### ✅ Задача:

Подписать доли прямо на секторы.

### 🔢 Пример:

```python
import matplotlib.pyplot as plt

labels = ['Apples', 'Bananas', 'Cherries', 'Dates']
sizes = [15, 30, 45, 10]

fig, ax = plt.subplots()
ax.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)

ax.axis('equal')  # круглая форма
plt.title("Круговая диаграмма с процентами")
plt.show()
```

### 💬 Комментарий:

- `autopct='%1.1f%%'` — автоматически добавляет значения (один знак после запятой).
- При необходимости можно передать функцию в `autopct`, чтобы кастомизировать текст (например, отображать абсолютные значения).
    
---

## 4️⃣ Диаграмма рассеяния (Scatter Plot)

### ✅ Задача:

Подписать отдельные точки.

### 🔢 Пример:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 25, 30]
labels = ['A', 'B', 'C', 'D']

fig, ax = plt.subplots()
ax.scatter(x, y, color='green')

# Добавление подписей
for i, label in enumerate(labels):
    ax.text(x[i] + 0.1, y[i], label, ha='left', va='center')

ax.set_title("Диаграмма рассеяния с подписями")
plt.show()
```

### 💬 Комментарий:

- Часто полезно добавлять небольшой сдвиг по `x`, чтобы текст не перекрывал маркер.

---

## 📐 Настройки стиля подписей

Параметры форматирования в `ax.text()`:

```python
fontsize=12, color='black', fontweight='bold', rotation=45
```

Пример:

```python
ax.text(x, y, 'Пример', fontsize=10, color='red', fontweight='bold', rotation=30)
```

---

## ⚙️ Продвинутый пример: использование `annotate()`

Для стрелок и уточнённого позиционирования:

```python
ax.annotate("Максимум", xy=(x_max, y_max), xytext=(x_max + 0.5, y_max + 5),
            arrowprops=dict(arrowstyle="->"), fontsize=10)
```

### 💬 Полезно при анализе временных рядов, экстремумов и т.п.

---
