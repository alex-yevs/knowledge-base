
Для создания виртуального окружения скачать файл по [ссылке](https://code.s3.yandex.net/data-analyst/da_practicum_env.yml). 
Этот файл содержит информацию о библиотеках, их версиях и названии окружения. Название файла - `da_practicum_env.yml`.

```yml
name: practicum
channels:
  - conda-forge
  - defaults
dependencies:
  - pip
  - ipykernel
  - ipython
  - ipython_genutils
  - jupyter
  - jupyter_client
  - jupyter_console
  - jupyter_core
  - jupyterlab
  - jupyterlab_server
  - requests
  - nest-asyncio
  - python=3.9
  - pip:
    - beautifulsoup4==4.9.3
    - matplotlib==3.3.4
    - nltk==3.6.1
    - numpy==1.20.1
    - pandas==1.2.4
    - plotly==5.4.0
    - psycopg2-binary==2.9.2
    - regex==2022.3.15
    - scikit-learn==0.24.1
    - scipy==1.8.0
    - seaborn==0.11.1
    - sqlalchemy==1.4.15
    - statsmodels==0.13.2
prefix: /opt/conda
```

### Создать виртуальное окружение

В терминале Anaconda Prompt:

```bash
conda env create -f путь 
```

, где `путь` - это путь до файла `da_practicum_env.yml`.

Например:

```bash
conda env create -f C:\Users\myuser\Downloads\da_practicum_env.yml 
```

❗**Возможная ошибка**

Если при установке окружения из файла возникнет ошибка **InvalidArchiveError:**
![](https://pictures.s3.yandex.net/resources/image_1698074935.png)

В этом случае очищаем временные файлы:

```bash
conda clean -a 
```

и пробуем снова создать окружение из файла `da_practicum_env.yml`.

### Активируем окружение

```bash
conda activate practicum 
```

## Установка `toc2` в Jupyter Notebook

Последние версии Jupyter Notebook не поддерживают модуль Jupyter Nbextensions. Поэтому придётся установить более старую версию:

```bash
pip install jupyter notebook==6.4.0 --user
```

Теперь можно установить Jupyter Nbextensions:

```bash
conda install -c conda-forge jupyter_contrib_nbextensions
```

Установить расширение для текущего пользователя:

```bash
jupyter contrib nbextension install --user
```

Установить панель управления расширениями:

```bash
conda install -c conda-forge jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
```

## Запускаем Jupyter Notebook

```bash
jupyter notebook
```

❗Если произошла ошибка `Module notebook.app not found`, то модуль `notebook.app` в указанном скрипте нужно переименовать в `notebook.notebookapp`. Это можно сделать вручную. В тексте ошибки будет путь к файлу `jupyter-notebook-script.py` со скриптом. Открой `jupyter-notebook-script.py` в текстовом редакторе и замени строку:

```bash
from notebook.app import main
```

на

```bash
from notebook.notebookapp import main
```

После этого сохрани файл и попробуй запустить Jupyter Notebook ещё раз в терминале Anaconda Prompt.

❗Если после этого при попытке запуска Jupyter Notebook возникнет ошибка `warn() missing 1 required keyword-only argument: stacklevel` или похожая на неё, попробуй выполнить две команды в терминале Anaconda Prompt при активированном виртуальном окружении:

```bash
pip uninstall traitlets
pip install traitlets==5.9.0
```

Теперь попробуй снова запустить Jupyter Notebook в терминале Anaconda Prompt.
### Если проблема с отображением sidebar `toc2`

Найти jupyter `custom.css` (если нет, создать), путь к custom CSS выглядит примерно так:

```bash
C:\Users\username\.jupyter\custom\custom.css
```

Добавить в `custom.css` следующий код:

```css
#toc-wrapper {
    top: 130px !important;
    z-index: 9999 !important;
}
```

ToC2 settings
![[Pasted image 20250518233029.png]]
![[Pasted image 20250518232948.png]]

## Установка `phik`

```bash
pip install phik
```



**datasets link**: 'https://code.s3.yandex.net/datasets/dataset_name.csv'
