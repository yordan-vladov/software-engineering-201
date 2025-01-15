# GitHub Actions

GitHub Actions е мощна платформа за автоматизация, която позволява на разработчиците да изграждат, тестват и внедряват своя код директно от своите GitHub хранилища. Работи, като дефинира действия с помощта на YAML файлове, съхранявани в директория `.github/workflows` в хранилище. Тези действия указват тригери, като push, pull или създаване на issue и дефинират задания, които се изпълняват във виртуални среди. Всяка задача се състои от стъпки, които могат да включват изпълнение на команди, изпълнение на скриптове или използване на многократно използвани GitHub Actions от GitHub Marketplace. Предоставяйки безпроблемна интеграция със събития на GitHub и обширна библиотека от предварително изградени действия, GitHub Actions позволява на екипите да рационализират непрекъсната интеграция (CI), непрекъсната доставка (CD) и други задачи за разработка с минимална настройка и максимална персонализация.

В това упражнение ще създадем Python проект, който ще се тества чрез GitHub Actions всеки път, когато е направена промяна в централното хранилище.

## Създаване на хранилище

Създайте хранилище `simple-calculator`, което да съдържа проект за прост калкулатор. Приложението ще се пише на Python и ще използва pytest за изпълняване на тестове, така че при създаване на хранилището добавете .gitignore файл с Python шаблон, както и лиценз по ваш избор.

## Създаване на проект

Клонирайте вашето хранилище и имплементирайте следната файлове структура:

```txt
simple-calculator
├── .github
│   └── workflows
│       └── python-tests.yml
├── LICENSE
├── requirements.txt
├── simple_calculator
│   ├── calculator.py
│   └── __init__.py
└── tests
    ├── __init__.py
    └── test_calculator.py
```

### simple_calculator

- Тази директория съдържа сорс кода на проекта:
    - **calculator.py** - съдържа функции за различните математични операции
    - **__init__.py** - празен файл, който маркира папката като пакет
```python
# simple_calculator/calculator.py

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```
## tests

- Тази директория съдържа тестовете за проекта:
    - **test_calculator.py** - съдържа фунцкии, които ще се изпълняват като тестове
    - **__init__.py** - празен файл, който маркира папката като пакет
```python
# tests/test_calculator.py
from simple_calculator.calculator import add, subtract

def test_add():
    assert add(1, 2) == 3

def test_subtract():
    assert subtract(5, 3) == 2
```

## .github/workflows

- Тази папка съдържа различните GitHub Actions, запазени в `.yml` файлове:
    -  **python-tests.yml** - GitHub Action, който автоматично изпълнява тестове всеки път е направена промяна към хранилището
```yml
name: Python Tests

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: "3.9"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Set PYTHONPATH to include src
        run: echo "PYTHONPATH=$(pwd)/src" >> $GITHUB_ENV

      - name: Run tests
        run: |
          pytest --maxfail=1 --disable-warnings -q
```

## requirements.txt

- Файл, който съдържа изисквания за pytest:
```txt
# requirements.txt
pytest==7.2.2
```

## Записване на промени

- Добавете направените промени, създайте нов запис и го добавете към централното хранилище.
- Отидете в страницата на хранилището в GitHub и провете дали GitHub Action-а се изпълнява и дали всички тестове минават. Провете **Actions** секцията на вашето хранилище.

## Добавяне на тестове

- Добавете към **tests/test_calculator.py** следният тест:
```python
def test_add_floats():
    assert add(0.1,0.2) == 0.3
```

- Добавете направените промени към GitHub и провете дали всички тестове минават.

## Предаване

- Качете линк към вашето хранилище.
