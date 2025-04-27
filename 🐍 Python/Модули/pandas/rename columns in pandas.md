В [[pandas]] есть несколько удобных способов переименовать столбцы. Вот основные:

#### 1. С помощью метода `.rename()`

Самый гибкий способ — использовать `.rename()`, передавая словарь `columns={старое_имя: новое_имя}`:

```python
import pandas as pd

df = pd.DataFrame({
    'A': [1, 2],
    'B': [3, 4]
})

df = df.rename(columns={'A': 'col1', 'B': 'col2'})
print(df)
```

Только указанные столбцы будут переименованы, остальные останутся без изменений.

---

#### 2. Просто переопределить `df.columns`

Если хочешь переименовать **все столбцы сразу**, можно задать новый список:

```python
df.columns = ['col1', 'col2']
print(df)
```

> [!warning] 
>  ⚡ Важно: список должен быть **той же длины**, что и количество столбцов.

---

#### 3. С помощью [[list comprehension]]

Если надо массово переименовать столбцы по какому-то шаблону:

```python
df.columns = [col.lower() for col in df.columns]
print(df)
```

Например, привести все имена к нижнему регистру.

---

#### 4. При чтении файла

Если создаёшь `DataFrame` из файла, можно переименовать столбцы сразу при загрузке:

```python
df = pd.read_csv('file.csv', names=['col1', 'col2'], header=0)
```

Тогда `header=0` говорит pandas, что первая строка — это заголовки, но мы их заменяем своими.

---

#### 5. Через `.set_axis()`

Можно использовать `.set_axis()`:

```python
df = df.set_axis(['col1', 'col2'], axis=1)
```

> [!warning] 
>  ⚡ Тоже требует полного списка новых имён.

---

> [!tip] 
>  ## Вот ещё полезные трюки для переименования столбцов в pandas:

#### 🔹 Заменить пробелы на подчёркивания

Иногда в названиях столбцов бывают пробелы, и хочется сделать их более "удобными":

```python
df.columns = df.columns.str.replace(' ', '_')
```

> [!note] 
>  👉 Теперь вместо `"Column Name"` будет `"Column_Name"`.

---

#### 🔹 Привести все имена к одному регистру (нижний или верхний)

Чтобы стандартизировать заголовки:

```python
df.columns = df.columns.str.lower()  # всё в нижний регистр
# или
df.columns = df.columns.str.upper()  # всё в верхний регистр
```

---

#### 🔹 Добавить префикс или суффикс к именам столбцов

Иногда надо явно отметить, что это, например, "новые" столбцы:

```python
df = df.add_prefix('new_')
# или
df = df.add_suffix('_2025')
```

> [!note] 
>  После `add_prefix('new_')`, столбец `"A"` превратится в `"new_A"`, и так далее.

---

#### 🔹 Комбинированная обработка: пробелы + регистр + префикс

Всё вместе в одну строчку:

```python
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_').str.replace(r'[^\w\s]', '')
```

> [!note] 
>  - `strip()` — убирает лишние пробелы с начала и конца
>  - `lower()` — делает строчные буквы
>  - `replace(' ', '_')` — заменяет пробелы на "_"
>  - `replace(r'[^\w\s]', '')` — убирает спецсимволы (если есть)

---

#### 🔥Как переименовать только те столбцы, которые соответствуют условию

Например, только те, что начинаются на `'old_'`:

```python
df = df.rename(columns=lambda x: x.replace('old_', '') if x.startswith('old_') else x)
```

---

#### 🔹 Переименование через `map` + `lambda`

Если нужно изменить **все** имена по какому-то правилу, можно использовать `map`:

```python
df.columns = df.columns.map(lambda x: x.upper())
```

👉 Превращаем все имена столбцов в ВЕРХНИЙ регистр.

Другой пример — добавить суффикс только к столбцам, содержащим `"sales"`:

```python
df.columns = df.columns.map(lambda x: x + '_USD' if 'sales' in x else x)
```

---

#### 🔹 Сложные переименования с помощью функции

Если обработка столбцов сложная, можно написать отдельную функцию:

```python
def clean_column_name(col):
    col = col.strip().lower().replace(' ', '_')
    if col.startswith('total_'):
        col = 'sum_' + col[6:]
    return col

df.columns = df.columns.map(clean_column_name)
```

👉 Тут мы:

- убираем пробелы,
- переводим в нижний регистр,
- и если столбец начинался на `total_`, заменяем на `sum_`.

---

#### 🔹 Только отдельные столбцы: через `.rename()` с функцией

Иногда хочется поменять имена **не всех столбцов**, а выборочно по условию:

```python
df = df.rename(columns=lambda x: x.replace('old_', '') if x.startswith('old_') else x)
```

Ещё вариант через словарь и генератор:

```python
df = df.rename(columns={col: col.replace(' ', '_') for col in df.columns if ' ' in col})
```

👉 Здесь мы переименуем только те, где есть пробелы.

---

#### 🔥 Ещё идея: цепочка через `pipe()`

Если хочется писать код суперчисто и красиво, можно использовать `pipe`:

```python
def rename_columns(df):
    df = df.rename(columns=lambda x: x.lower().replace(' ', '_'))
    return df

df = (df
      .pipe(rename_columns)
     )
```

> [!note] 
>  `pipe` даёт возможность применять цепочку функций к `DataFrame`'у — особенно классно для больших пайплайнов.

---

> [!example] 
> ## Примеры, полезные в реальных кейсах: 

#### 📈 1. Подготовка данных для моделей машинного обучения (ML)

**Проблема:**  
Модели типа `scikit-learn`, `xgboost`, `lightgbm` не любят, когда в названиях столбцов есть:

- Пробелы
- Заглавные буквы
- Русские символы
- Спецзнаки типа `$`, `%`, `#`

**Решение:**  
Перед обучением модели полезно делать "очистку" названий столбцов:

```python
def clean_columns(df):
    return df.rename(columns=lambda x: x.strip()
                                           .lower()
                                           .replace(' ', '_')
                                           .replace('%', 'percent')
                                           .replace('$', 'usd')
                                           .replace('#', 'number'))

df = clean_columns(df)
```

**Что получается:**

- `Total Sales ($)` → `total_sales_usd`
- `Profit %` → `profit_percent`
- `Employee#` → `employee_number`

---

#### 📊 2. Подготовка данных для отчётов в Excel/Google Sheets

**Проблема:**  
В реальных проектах часто нужно готовить отчёты в Excel для руководства или клиентов.  
Excel нормально отображает только "человеческие" названия колонок.

**Решение:**  
Делаем "красивое" переименование для отчётов:

```python
column_mapping = {
    'client_id': 'Client ID',
    'purchase_amount_usd': 'Purchase Amount (USD)',
    'signup_date': 'Signup Date'
}

df = df.rename(columns=column_mapping)
```

👉 Таким образом, отчёт становится понятным даже для "нематематиков".

---

#### 🏗️ 3. Когда объединяешь много разных датасетов

**Проблема:**  
Ты загружаешь несколько таблиц, а в одной столбец называется `user_id`, а в другой `User_ID`.

**Решение:**  
Перед `concat`, `merge` или `join` нужно стандартизировать названия:

```python
def standardize_columns(df):
    return df.rename(columns=lambda x: x.lower().strip())

df1 = standardize_columns(df1)
df2 = standardize_columns(df2)

df_combined = pd.concat([df1, df2])
```

---

#### 🛠️ 4. Автоматическая замена колонок для SQL-интеграции

**Проблема:**  
Если выгружаешь pandas-таблицу в базу данных через `.to_sql()`, столбцы должны быть в формате без спецсимволов и лучше маленькими буквами.

**Решение:**  
Тут без массового переименования тоже никак:

```python
df.columns = [col.lower().replace(' ', '_').replace('-', '_') for col in df.columns]
```

---

> [!example] 
>  #### ⚡ Мини-пример "жизни":

```python
import pandas as pd

df = pd.DataFrame({
    'User ID': [1, 2],
    'Purchase Amount ($)': [100, 150],
    'Signup Date': ['2025-01-01', '2025-01-02']
})

df_clean = (df
            .rename(columns=lambda x: x.lower().replace(' ', '_').replace('($)', 'usd').replace('(', '').replace(')', ''))
           )

print(df_clean)
```

**Вывод:**
```console black:1-3
   user_id  purchase_amount_usd signup_date
0        1                 100   2025-01-01
1        2                 150   2025-01-02
```

---
> [!example] 
>  #### **Универсальная функция** для переименования столбцов в pandas, которую реально можно копировать себе в проекты:

Как можно сделать "универссальную-функцию", чтобы сразу:

- загрузить датафрейм (`read_csv`, `read_excel` и т.п.)
- и сразу же почистить названия столбцов на лету.

---


```python
import pandas as pd
import re

def clean_column_names(df, *,
                        lowercase=True,
                        replace_spaces=True,
                        replace_special_chars=True,
                        custom_replacements=None,
                        prefix=None,
                        suffix=None):
    """
    Универсальная очистка названий колонок DataFrame.

    Параметры:
    - lowercase: привести к нижнему регистру
    - replace_spaces: заменить пробелы на _
    - replace_special_chars: удалить спецсимволы
	  (оставить только буквы, цифры, _)
    - custom_replacements: словарь {'что_заменить': 'на_что'}
    - prefix: добавить префикс ко всем колонкам
    - suffix: добавить суффикс ко всем колонкам
    """
    
    new_columns = df.columns
    
    if lowercase:
        new_columns = new_columns.str.lower()
        
    if replace_spaces:
        new_columns = new_columns.str.replace(' ', '_', regex=False)
        
    if replace_special_chars:
        new_columns = new_columns.map(lambda x: re.sub(r'[^\w]', '', x))
        
    if custom_replacements:
        for old, new in custom_replacements.items():
            new_columns = new_columns.str.replace(old, new, regex=True)
    
    if prefix:
        new_columns = prefix + new_columns
    
    if suffix:
        new_columns = new_columns + suffix
    
    df = df.copy()
    df.columns = new_columns
    return df

def read_and_clean(filepath, *, 
                   filetype='csv', 
                   **clean_kwargs):
    """
    Загружает файл и сразу чистит названия колонок.

    filetype: 'csv' или 'excel'
    clean_kwargs: передаются в clean_column_names
    """
    if filetype == 'csv':
        df = pd.read_csv(filepath)
    elif filetype == 'excel':
        df = pd.read_excel(filepath)
    else:
        raise ValueError("filetype должен быть 'csv' или 'excel'")
    
    df = clean_column_names(df, **clean_kwargs)
    return df
```

---

#### Как использовать:

**Пример 1: Просто загрузить CSV и почистить**

```python
df = read_and_clean('data.csv')
```

**Пример 2: Загрузить Excel и добавить префикс ко всем колонкам**

```python
df = read_and_clean('data.xlsx', filetype='excel', prefix='raw_')
```

**Пример 3: Загрузить CSV и убрать спецсимволы, добавить свои замены**

```python
df = read_and_clean('sales_data.csv', 
                    custom_replacements={'usd': 'dollar', 'qty': 'quantity'})
```

---
