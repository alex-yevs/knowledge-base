
Установи [[uv]] по инструкции с сайта:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

После установки обнови окружение и проверь, что утилита работает:
```bash
source ~/.bashrc
uv --version  # uv 0.6.17
```

Создай директорию проекта и запусти инициализацию в корне проекта:
```bash
mkdir uv-project
cd uv-project
uv init
```

В результате менеджер создаст такую структуру директорий:
```console black:1-5
.
├── .python-version
├── README.md
├── main.py
└── pyproject.toml
```

Удали шаблонный `main.py` и создай поддиректорию проекта, где будут храниться все модули:
```console black:1-6
.
├── .gitignore
├── .python-version
├── README.md
├── pyproject.toml
└── uv_project
```

Такая структура разделяет компоненты с рабочим кодом от общих компонентов настройки проекта. Так все модули нашего приложения будут лежать в директории проекта `uvproject`. А все файлы конфигурации проекта лежат в корне.

Среди этих файлов _README.md_ - текстовое описание нашего проекта, _.python-version_ - файл с указанием версии [[Python]], нужен для установки проекта, и _pyproject.toml_ - файл с описанием метаданных и настроек нашего проекта. Рассмотрим его подробнее:
```toml
[project]
name = "uv-project"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []
```

_pyproject.toml_ — это текстовый файл, внутри которого данные хранятся в [[TOML]] формате. Строчки вида `[project]` описывают секции с парами `ключ = "значение"`. В примере выше значением ключа `name` будет `"uv-project"`.

Самая важная секция сейчас - `[project]`. В ней описываются общие данные проекта. Здесь хранится версия `version`, описание `description`, название `name`. Также указана требуемая [[версия Python]] `requires-python` и список зависимостей `dependencies`.

После завершения процесса инициализации можно приступать к самому главному — написанию кода. Открой проект в редакторе, это можно сделать командой `code .` и создай в поддиректории проекта новый файл _example.py_. Добавь в него необходимый код (хотя бы вывод для начала `print("Hello!")` и запусти. Запускать код нужно обязательно из корневой директории проекта, указывая полный путь от нее до файла:
```bash
python3 uv_project/example.py
```

Затем сделай коммит в [[git]].