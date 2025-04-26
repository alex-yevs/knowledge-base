
🕰️ Модуль `datetime` в стандартной библиотеке Python предоставляет классы и функции для работы с датой, временем и их комбинациями. Он особенно полезен при обработке временных меток, вычислениях с датами и форматировании времени.

---

## 📦 Структура модуля `datetime`

Модуль предоставляет несколько ключевых классов:

|Класс|Назначение|
|---|---|
|`datetime.date`|Представляет календарную дату (год, месяц, день)|
|`datetime.time`|Представляет время (часы, минуты, секунды, микросекунды)|
|`datetime.datetime`|Комбинация даты и времени|
|`datetime.timedelta`|Разница между двумя объектами `date` или `datetime`|
|`datetime.tzinfo`|Абстрактный базовый класс для работы с часовыми поясами|
|`datetime.timezone`|Конкретная реализация `tzinfo` (с поддержкой смещения)|

---

## 📅 1. Работа с датами: `datetime.date`

```python
from datetime import date

today = date.today()  # Получить текущую дату
print(today)          # Например: 2025-04-26

# Создание конкретной даты
some_date = date(2023, 12, 31)

# Получение компонентов
print(some_date.year, some_date.month, some_date.day)
```

🔍 **Зачем это нужно:** удобно для бизнес-логики, валидации, логирования и сравнения дат.

---

## 🕒 2. Работа со временем: `datetime.time`

```python
from datetime import time

t = time(14, 30, 15)  # Часы, минуты, секунды
print(t.hour, t.minute, t.second)  # 14 30 15
```

> 🛠 **Практика:** `time` используется реже, чаще — вместе с `datetime`.

---

## 📆🕔 3. Комбинирование даты и времени: `datetime.datetime`

```python
from datetime import datetime

now = datetime.now()       # Локальное текущее дата и время
utc_now = datetime.utcnow()  # Время по UTC

# Создание объекта вручную
dt = datetime(2024, 5, 10, 9, 30)
```

📌 **Форматирование и разбор строк:**

```python
# Форматирование в строку
formatted = dt.strftime("%Y-%m-%d %H:%M:%S")
print(formatted)  # '2024-05-10 09:30:00'

# Разбор строки в datetime
parsed = datetime.strptime("2024-05-10 09:30:00", "%Y-%m-%d %H:%M:%S")
```

📚 **Документация по форматам**: [strftime() и strptime() Format Codes](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes)

---

## ➖ 4. Работа с интервалами: `datetime.timedelta`

```python
from datetime import datetime, timedelta

delta = timedelta(days=5, hours=3)
future = datetime.now() + delta
past = datetime.now() - timedelta(weeks=1)

print(future, past)
```

🔧 **На практике:** используйте `timedelta` для планирования, дедлайнов, сдвига дат.

---

## 🌍 5. Работа с часовыми поясами

#### `timezone.utc` и смещения

```python
from datetime import datetime, timezone

dt_utc = datetime.now(timezone.utc)
print(dt_utc.isoformat())  # Например: 2025-04-26T12:34:56.789012+00:00
```

#### Локализация с помощью сторонних библиотек (например, `pytz`, `zoneinfo` в Python 3.9+)

```python
# Python 3.9+ — встроенный модуль zoneinfo
from zoneinfo import ZoneInfo

dt_local = datetime(2025, 4, 26, 15, 0, tzinfo=ZoneInfo("Europe/Moscow"))
print(dt_local.isoformat())
```

> ⚠️ **Важно:** для корректной работы с часовыми поясами в продакшене — всегда используйте `tzinfo`.

---

## ✅ Лучшие практики

#### 1. Используйте `datetime` с `tzinfo`, чтобы избежать ошибок при вычислениях и сравнениях.

```python
# Плохо: нативный datetime
dt1 = datetime(2025, 4, 26, 15, 0)

# Хорошо: datetime с tzinfo
dt2 = datetime(2025, 4, 26, 15, 0, tzinfo=timezone.utc)
```

#### 2. Никогда не сравнивайте datetime и datetime с timezone объекты.

```python
# Это вызовет исключение
datetime(2025, 4, 26) < datetime.now(timezone.utc)
```

#### 3. Для хранения в БД или обмена через API — используйте ISO 8601 (`.isoformat()` или `strftime`).

#### 4. Для бизнес-логики всегда используйте `timedelta`, а не «ручные» вычисления времени.

#### 5. Избегайте хардкода часовых поясов — используйте `zoneinfo` или `pytz` (в старых проектах).

---

## 📌 Заключение

Модуль `datetime` — мощный инструмент для работы с временем и датами в Python. Глубокое понимание его классов и соблюдение лучших практик поможет избежать типичных ошибок: неправильного сравнения дат, проблем с часовыми поясами и некорректного форматирования.
