# Лабораторная работа 5
Git advanced workshop

## Предварительные требования:

⋅⋅⋅Основы работы с Git (лабораторная работа по введению в Git).
⋅⋅⋅Установленный Git на локальной машине.


## Введение

1. Создание репозитория на GitHub:

    Зайдите в свою учетную запись GitHub и создайте новый репозиторий, например, с именем git-practice.
    Скопируйте URL вашего репозитория.

2. Клонирование репозитория:

    Откройте терминал и перейдите в папку, где вы хотите сохранить локальную копию репозитория.
    Введите следующие команды, используя скопированный URL:

    ```
    git clone <URL-репозитория>
    cd git-lab
    ```

3. Добавление файла:

    Создайте новый текстовый файл, например, example.txt, и добавьте в него какой-то текст, например, структуру книги (главы, параграфы...)
    Вернитесь в терминал и введите:

    ```
    git add example.txt
    git commit -m "File added example.txt"
    git push origin main
    ```

4. Создание ветки:

    Создайте новую ветку с названием, например, ```feature-branch```, и переключитесь на нее:
    
    ```
    git branch feature-branch
    git checkout feature-branch
    ```

5. Отредактируйте файл example.txt, добавив еще текст.

    Повторите шаги, указанные в п. 3. Имя коммита должно отличаться!

6. Слияние изменений:

    Переключитесь обратно в основную ветку:
    
    ```
    git checkout main
    ```
    Слейте изменения из ветки ```feature-branch``` в основную ветку:

    ```
    git merge feature-branch
    git push origin main
    ```

7. Завершение:

    Проверьте, что изменения успешно слиты и отображаются в основной ветке на GitHub.
    Завершите работу с репозиторием.

## Работа с ветками

1. Создайте новый текстовый файл с базовой структурой книги, например:

```
# Название книги

## Глава 1: Введение
Здесь будет введение в тему книги.

## Глава 2: Основы Git
Основные понятия и команды Git.

```

2. Создайте ветку "feature-login" для разработки новой функциональности:

```
git checkout -b feature-login
```

3. Внесите изменения в файл:

```
# Название книги

## Глава 1: Введение
Здесь будет введение в тему книги.

## Глава 2: Основы Git
Основные понятия и команды Git.

## Глава 3: Вход в систему
Раздел по новой функциональности входа в систему.
```

4. Завершите изменения, закоммитьте их и отправьте ветку на GitHub:

```
git add README.md
git commit -m "Добавлена глава 3: Вход в систему"
git push origin feature-login
```

## Работа с удаленным репозиторием

1. Переключитесь на основную ветку (main) и внесите изменения:

```
git checkout main
```

2. Внесите изменения в основной ветке (например, добавьте описание книги):

```
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git
Основные понятия и команды Git.

```

3. Закоммитьте изменения и отправьте их на GitHub:

```
git add <filename>
git commit -m "Изменено название книги и введение"
git push origin main

```


## Моделирование конфликта

1. Вернитесь в ветку "feature-login" и внесите изменения в том же участке:

```
git checkout feature-login
```

2. Измените главу 2 в файле

```
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.

```

3. Закоммитьте изменения и отправьте их на GitHub:

```
git add README.md
git commit -m "Добавлен раздел о магии конфликтов"
git push origin feature-login

```

## Разрешение конфликта

1. Вернитесь в основную ветку и попробуйте слить изменения:

```
git checkout main
git pull origin main
```

2. Возникнет конфликт. Разрешите его в файле

```
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

<<<<<<< HEAD
## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.
======= 
## Глава 2: Основы Git
Основные понятия и команды Git. 
>>>>>>> feature-login

```

3. Разрешите конфликт, удалив метки и оставив нужные изменения:

```
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.
```

4. Закоммитьте разрешение конфликта и отправьте изменения на GitHub:

```
git add README.md
git commit -m "Resolved conflict in chapter 2"
git push origin main

```

## Автоматизация проверки формата файлов при коммите

Хорошо, предположим, у вас есть задача автоматизировать проверку формата файлов при коммите с использованием Git Hooks. Давайте создадим простую задачу и решение для этого случая.

1. Задача

Перед каждым коммитом необходимо автоматически проверять, чтобы все .txt файлы в репозитории соответствовали определенному формату.

2. Решение

  * Создайте скрипт (например, check_format.sh), который будет выполнять проверку формата .txt файлов. Этот скрипт может использовать инструменты, такие как grep или другие, чтобы проверить соответствие формату.

```
#!/bin/bash

for file in $(git diff --cached --name-only | grep '\.txt$'); do
    if ! some_format_check_command "$file"; then
        echo "Ошибка: Файл $file не соответствует формату."
        exit 1
    fi
done

``` 
  * Добавление скрипта в репозиторий.
    Поместите скрипт в папку, например, в .git/hooks и назовите его pre-commit. Убедитесь, что у него есть права на выполнение.

    ```
    cp check_format.sh .git/hooks/pre-commit
    chmod +x .git/hooks/pre-commit

    ```

  * Попробуйте внести изменения и закоммитить.

    Теперь, при каждой попытке закоммитить изменения, Git будет автоматически выполнять проверку формата файлов перед коммитом. 

    ```
    git add .
    git commit -m "Добавлены изменения"

    ```
  * Шаг 4: Решение конфликтов (если необходимо).

    Если вам необходимо внести изменения в файлы, чтобы они соответствовали формату, внесите изменения, добавьте файлы и снова попробуйте закоммитить. 

3. Примечание:

В данном примере использован условный синтаксис, предполагая, что у вас есть спецификация формата файла, которую можно проверить с использованием инструментов командной строки. Реальная проверка будет зависеть от конкретных требований вашего проекта.

## Использование Git Flow в проекте

Задача: интегрировать Git Flow в проект для управления циклом разработки, создания релизов и управления hotfixes. 
Предположим, у вас есть задача на создание новой функциональности для вашего проекта с использованием Git Flow. Давайте рассмотрим конкретный пример.

1. Убедитесь, что Git Flow установлен на локальной машине:

```
sudo apt-get install git-flow
```

2. В корне репозитория выполните инициализацию Git Flow.

```
git flow init
```

3. Создайте ветку для новой функциональности "task-management":

```
git flow feature start task-management
```

4. Внесите изменения в код для добавления функционала управления задачами (например, в файл task_manager.py):

```
# task_manager.py

def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")

```

Выполните коммит изменения по мере разработки:

```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"


```

5. После завершения разработки функции завершите фичу и объедините ее с основной веткой:

```
git flow feature finish task-management

```

Git Flow автоматически переключится на ветку develop и выполнит слияние. Если есть конфликты, их нужно разрешить.

6. Переключитесь на ветку "develop" и начните создание релиза:

```
git checkout develop
git flow release start v1.0.0
```

7. Внесите изменения, связанные с релизом (например, обновите версию в файле version.txt):

```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"

```

8. Завершите релиз и объедините его с ветками "develop" и "main":

```
git flow release finish v1.0.0
```

9. Если в процессе использования выявлена критическая ошибка, создайте hotfix:

```
git flow hotfix start hotfix-1.0.1
```

10. Внесите изменения для исправления ошибки и коммитите:

```
# Исправление ошибки
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```

11. Завершите hotfix и объедините его с ветками "develop" и "main":

```
git flow hotfix finish hotfix-1.0.1
```

12. Завершение работы и отправка изменений на удаленный репозиторий. Отправьте изменения на удаленный репозиторий:

```
git push origin develop
git push origin main

```