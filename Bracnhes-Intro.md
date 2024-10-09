# Разклонения в Git

В това упражнение ще създадете и управлявате Git хранилище, за изграждане на проста HTML уеб страница. Проектът ще включва създаване на функции като лента за навигация, хедър и футър с помощта на отделни клонове.

## Нужни команди

### 1. **`git init`**

Инициализира ново Git хранилище в текущата директория. Това създава папката `.git`, което позволява на Git да проследява промените в проекта.

### 2. **`git add <file>`**

Етапни промени (нови файлове или модификации) за следващия комит. В този случай `git add index.html` поставя файла `index.html` да бъде включен в следващия комит.

### 3. **`git commit -m "message"`**

Записва поетапните промени в хронологията на хранилището, заедно със съобщение, описващо промените. Флагът `-m` ви позволява да добавите съобщение за ангажиране в кавички.

### 4. **`git checkout -b <branch-name>`**

Създава нов клон и превключва към него. Например `git checkout -b add-navbar` създава и премества към клон с име `add-navbar`.

### 5. **`git checkout <branch-name>`**

Превключва към съществуващ клон. Например `git checkout main` превключва обратно към клона `main`.

### 6. **`git merge <branch-name>`**

Комбинира промените от посочения клон в текущия клон. Например `git merge add-navbar` обединява промените от клона `add-navbar` в текущия клон (напр. `main`).

### 9. **`git add .`**

Подрежда всички промени (във всички файлове) в текущата директория за следващия комит. Това е полезно за ангажиране на множество файлове наведнъж.

### 10. **`git remote add origin <URL>`**

Свързва вашето локално хранилище с отдалечено хранилище (в този случай в GitHub). Този URL е мястото, където ще бъдат изпратени локалните промени.

### 11. **`git push -u origin main`**

Избутва `главния` клон към отдалеченото хранилище. Флагът `-u` задава хранилището `origin` като дистанционно хранилище по подразбиране за бъдещи натискания.

### 12. **`git push origin <branch>`**

Избутва специфичен клон (напр. `add-navbar`, `add-header`) към отдалеченото хранилище.

## 1. Инициализация на Git хранилище

1. Създайте нова директория и навигирайте към нея

```bash
mkdir git-branch-exercise && cd git-branch-exercise
```

2. Инициализирайте Git хранилище

```bash
git init
```

3. Създайте `index.hmtl` файл със следното съдържание:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Git Branching Exercise</title>
</head>
<body>
    <h1>Welcome to our webpage!</h1>
</body>
</html>
```

Това ще служи като скелет за вашата уеб страница

4. Добавете и запишете първоначалните промени:

```bash
git add index.html
git commit -m "Initial commit: basic HTML structure"
```

## 2. Създаване на клони

Сега си представете, че работите върху три различни функции: лента за навигация, хедър и футър. Тези функции ще бъдат разработени в отделни клонове.

1. Създайте нов клон за навигация:

```bash
git checkout -b add-navbar
```

2. В `add-navbar` клонът, модифицирайте `index.html` като добавите `<nav>` секция:

```html
<nav>
    <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</nav>
```

3. Запишете промените:

```bash
git add index.html
git commit -m "Add navigation bar"
```

4. Създайте клон, в който ще разработите хедъра:

```bash
git checkout main
git checkout -b add-header
```

5. В `add-header` клонът, добавете хедър в `index.html`:

```html
<header>
    <h1>This is the header section</h1>
</header>
```

6. Запишете промените:

```bash
git add index.html
git commit -m "Add header section"
```

7. Създайте клон, в който ще разработите футъра:

```bash
git checkout main
git checkout -b add-footer
```

8. В `add-footer` клонът, добавете футър в `index.html`:

```hmtl
<footer>
    <p>&copy; 2024 My Website</p>
</footer>
```

9. Запишете промените:

```bash
git add index.html
git commit -m "Add footer section"
```

## 3. Сливане на промените

Сега, когато всички функции са внедрени в отделни клонове, е време да ги обединим в `main` клона.


1. Сливане на `add-navbar`

```bash
git checkout main
git merge add-navbar
```

2. Сливане на `add-header`:

```bash
git merge add-header
```

3. Merge the `add-footer` branch:

```bash
git merge add-footer
```

4. Ако има някакви конфликти (напр. множество клонове, модифициращи една и съща секция на index.html), разрешите конфликтите, като редактирате файла, след което:

```bash
git add index.html
git commit -m "Resolved merge conflicts"
```

## 4. Качване към централно хранилище

1. **Създайте ново хранилище в GitHub** (без да го инициализирате с README).
2. **Добавете URL-а** (заменете `<username>` и `<repository>` с вашето GitHub потребителско име и име на хранилище):
   
```bash
git remote add origin https://github.com/<username>/<repository>.git
```

3. Изпратете клоновете към GitHub:
   
```bash
git push -u origin main
git push origin add-navbar
git push origin add-header
git push origin add-footer
```
## 5. Бонус задача

1. Създайте нов клон `add-styles`, за да добавите CSS стил за уеб страницата. Променете HTML, за да свържете файл `styles.css`.
2. Обвържете промените.
3. Обединете клона `add-styles` в `main`.
4. Запишете промените и ги добавете към GitHub

