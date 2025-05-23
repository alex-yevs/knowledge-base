
📚 **SQL (Structured Query Language)** — это стандартный язык для взаимодействия с реляционными базами данных.  
Он используется для создания, изменения, управления и извлечения данных.

🔹 **Основные задачи SQL**:

- Определение структуры данных (`DDL`: Data Definition Language)
- Управление данными (`DML`: Data Manipulation Language)
- Управление доступом (`DCL`: Data Control Language)
- Работа с транзакциями (`TCL`: Transaction Control Language)

---

## 2. Основные компоненты SQL

#### 2.1 DDL — Определение структуры данных

Команды для создания и изменения схемы базы данных:

|Команда|Назначение|
|:--|:--|
|`CREATE`|Создание объектов (таблиц, схем)|
|`ALTER`|Изменение структуры объектов|
|`DROP`|Удаление объектов|
|`TRUNCATE`|Очистка таблицы без удаления структуры|

▶️ **Пример**:

```sql
-- Создание таблицы пользователей
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

#### 2.2 DML — Манипуляция данными

Операции добавления, изменения, удаления записей:

|Команда|Назначение|
|:--|:--|
|`SELECT`|Извлечение данных|
|`INSERT`|Добавление данных|
|`UPDATE`|Обновление данных|
|`DELETE`|Удаление данных|

▶️ **Пример**:

```sql
-- Добавление нового пользователя
INSERT INTO users (id, name, email)
VALUES (1, 'Alice Johnson', 'alice@example.com');
```

---

#### 2.3 DCL — Управление доступом

Команды безопасности:

|Команда|Назначение|
|:--|:--|
|`GRANT`|Предоставление прав|
|`REVOKE`|Отзыв прав|

▶️ **Пример**:

```sql
-- Разрешение пользователю читать данные
GRANT SELECT ON users TO readonly_user;
```

---

#### 2.4 TCL — Управление транзакциями

Контроль целостности операций:

|Команда|Назначение|
|:--|:--|
|`BEGIN`|Начало транзакции|
|`COMMIT`|Подтверждение изменений|
|`ROLLBACK`|Откат изменений|

▶️ **Пример**:

```sql
-- Обработка транзакции
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

---

## 3. Ключевые концепции SQL

#### 3.1 Первичные ключи и внешние ключи

- **PRIMARY KEY** — уникальный идентификатор записи.
- **FOREIGN KEY** — ссылка на первичный ключ другой таблицы.

▶️ **Пример связи**:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    amount DECIMAL(10, 2),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

> [!warning] 
>  **Важно**: Использование внешних ключей обеспечивает целостность данных между таблицами.

---

#### 3.2 Индексы

Индексы ускоряют поиск данных, но увеличивают стоимость операций вставки/обновления.

▶️ **Создание индекса**:

```sql
CREATE INDEX idx_users_email ON users(email);
```

> [!tip] 
>  **Рекомендация**: Индексируйте поля, которые часто участвуют в фильтрации (`WHERE`) или соединениях (`JOIN`).

---

#### 3.3 Нормализация данных

Процесс оптимизации структуры таблиц для устранения избыточности и зависимостей.

- **Первая нормальная форма (1NF)**: атомарность данных.
- **Вторая нормальная форма (2NF)**: устранение частичных зависимостей.
- **Третья нормальная форма (3NF)**: устранение транзитивных зависимостей.

> [!note] 
>  **На практике**: легкая денормализация допустима для повышения производительности чтения.

---

## 4. Лучшие практики работы с SQL

#### 4.1 Чистота и читаемость запросов

- Используйте **чёткие отступы** и **ключевые слова в верхнем регистре**.
- Разбивайте длинные запросы на логические блоки.

 ▶️ **Плохо**:

```sql
select * from users where id=1;
```

▶️ **Хорошо**:

```sql
SELECT *
FROM users
WHERE id = 1;
```

---

#### 4.2 Явное указание колонок

Избегайте `SELECT *`, чтобы:

- Уменьшить объем передаваемых данных
- Повысить ясность запроса
- Стабилизировать код при изменении схемы

▶️ **Пример**:

```sql
SELECT id, name, email
FROM users
WHERE active = true;
```

---

#### 4.3 Использование параметризированных запросов

Для предотвращения SQL-инъекций всегда используйте параметризацию:

▶️ **На Python с использованием библиотеки `psycopg2`**:

```python
cursor.execute(
    "SELECT * FROM users WHERE email = %s",
    (user_email,)
)
```

---

#### 4.4 Оптимизация запросов

- Избегайте ненужных вложенных подзапросов.
- Анализируйте планы выполнения (`EXPLAIN`).
- Используйте агрегатные функции аккуратно.

▶️ **Анализ запроса**:

```sql
EXPLAIN ANALYZE
SELECT name FROM users WHERE email = 'alice@example.com';
```

---

#### 4.5 Работа с транзакциями

Группируйте логически связанные операции в транзакции, чтобы:

- Обеспечить целостность данных
- Упростить откат в случае ошибок

---

## 5. Заключение

SQL — это основа работы с данными в современных информационных системах.  
Грамотное владение SQL позволяет:

- Писать надёжные и производительные запросы
- Строить масштабируемые архитектуры хранения данных
- Защищать приложения от уязвимостей и ошибок

**Хорошая практика**: всегда думать об оптимизации, читаемости и безопасности ваших SQL-скриптов.
