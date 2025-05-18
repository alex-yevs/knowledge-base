Для создания виртуального окружения скачать файл по [ссылке](https://code.s3.yandex.net/data-analyst/da_practicum_env.yml). Этот файл содержит информацию о библиотеках, их версиях и названии окружения. Название файла - `da_practicum_env.yml`.

## Создать виртуальное окружение

В терминале Anaconda Prompt:

```bash
conda env create -f путь 
```

, где `путь` - это путь до файла `da_practicum_env.yml`.

Например:

```bash
conda env create -f C:\Users\myuser\Downloads\da_practicum_env.yml 
```

**Возможная ошибка**

Если при установке окружения из файла возникнет ошибка **InvalidArchiveError:**
![](https://pictures.s3.yandex.net/resources/image_1698074935.png)

В этом случае очищаем временные файлы:

```bash
conda clean -a 
```

и пробуем снова создать окружение из файла `da_practicum_env.yml`.

## Активируем окружение

```bash
conda activate practicum 
```

## Запускаем Jupyter Notebook

```bash
jupyter notebook
```




**datasets link**: 'https://code.s3.yandex.net/datasets/dataset_name.csv'
