# Разклонения с git rebase

В това упражнение ще вземете съществуващ код и ще го подобрите. Добра практика е код да се качва в основният клон. За тази цел, когато правите промяна, ще създадете нов клон, ще направите промяната в новият клон, и ще слеете новият клон с  main. Това упражнение всички промени, които правите, ще бъдат с `git rebase`.

`git rebase` е команда, която премества основата на вашия клон към друг клон, възпроизвеждайки вашите записи върху него, което води до по-чиста, линейна хронология на ангажименти без комити за сливане. Обикновено се използва за интегриране на промени от базов клон (като `main`) в клон на функция, без да се въвежда ангажимент за сливане. Въпреки че поддържа хронологията подредена, преподреждането пренаписва хронологията на ангажиментите, така че трябва да се използва предпазливо, особено с разклонения, споделени с други. Можете също така да използвате интерактивно повторно базиране (`git rebase -i`), за да редактирате, пренаредите или премахнете записи по време на процеса.

## 1. Инициализация на Git хранилище

1. **Инициализация на хранилище**: Направете **fork** на [следното хранилище](https://github.com/yordan-vladov/example-html) в GitHub. Клонирайте вашето хранилище и влезте в него.
   ```bash
   git clone <вашето хранилище>
   cd <вашето хранилище>
   ```

## 2. Прост Rebase
1. **Създаване на нов клон**: Създайте нов клон `feature/update-title`.
   ```bash
   git checkout -b feature/update-title
   ```

2. **Промяна на заглавие**: В `index.html` променете `<title>` елементът на:
   ```html
   <title>Updated Title - Git Exercise</title>
   ```

3. **Запис на промяната**:
   ```bash
   git add index.html
   git commit -m "Update page title in index.html"
   ```

4. **Върнете се към main**:
   ```bash
   git checkout main
   ```

5. **Rebase**: Пренаредете клонът `feature/update-title` в `main`.
   ```bash
   git rebase feature/update-title
   ```

## 3. Rebase с няколко записа (промяна на HTML & CSS)
1. **Нов клон**: Създайте нов клон `feature/update-header`.
   ```bash
   git checkout -b feature/update-header
   ```

2. **Модифициране на текст**: В `index.html`, променете текста в `<header>` елемента:
   ```html
   <h1>Welcome to the Git Exercise Page</h1>
   ```

3. **Запис на промяната**:
   ```bash
   git add index.html
   git commit -m "Update header text in index.html"
   ```

4. **Модифициране на цвят в CSS**: В `style.css`, променете цветът на фонът на `header` на по-светъл цвят:
   ```css
   header {
       background-color: #3b5998;
	   ...
   }
   ```

5. **Запис на промяната**:
   ```bash
   git add style.css
   git commit -m "Update header background color in style.css"
   ```

6. **Rebase**: Пренаредете клонът  `feature/update-header` в `main.
   ```bash
   git checkout main
   git rebase feature/update-header
   ```

## 4. Интерактивен rebase (Сплескване на записи)
1. **Нов клон**: създайте нов клон `feature/add-footer-content`.
   ```bash
   git checkout -b feature/add-footer-content
   ```

2. **Добавяне на абзац**: Добавете нов абзац към `footer` секцията на `index.html`:
   ```html
   <p>All rights reserved 2024.</p>
   ```

3. **Запис на промяната**:
   ```bash
   git add index.html
   git commit -m "Add footer copyright paragraph"
   ```

4. **Добавяне на още съдържание**: Добавете линк към политика за сигурност:
   ```html
   <p><a href="#">Privacy Policy</a></p>
   ```

5. **Запис на промяната**:
   ```bash
   git add index.html
   git commit -m "Add privacy policy link to footer"
   ```

6. **Интерактивен Rebase**: Използвайте `git rebase -i` за да сплескате два записа в един.
   ```bash
   git rebase -i HEAD~2
   ```

   Когато бъдете подканени, смачкайте втория запис в първия и актуализирайте съобщението.

7. **Rebase**: Пренаредете клонът  `feature/update-footer` в `main.
   ```bash
   git checkout main
   git rebase feature/add-footer-content
   ```

## 6. Rebase с няколко клона (Интеграция на функционалности)
1. **Създаване на клони за фунцкионалности**:
   - Създайте клон `feature/add-about-page` за създаване на файл `about.html`.
   - Създайте клон `feature/change-font` за модифициране на `style.css`.

2. **Работа в `feature/add-about-page`**:
   - Създайте `about.html`:
     ```html
     <!doctype html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>About Us</title>
     </head>
     <body>
         <h1>About Our Website</h1>
     </body>
     </html>
     ```
   - Променете линка в `index.html` да сочи към `about.html`
   - Запишете промяната.

3. **Работа в `feature/change-font`**:
   - Променете `style.css`. Направете `font-family` да бъде `Georgia, serif`.
   - Запишете промяната.

4. **Rebase на клоните**:
   - Пренаредете `feature/change-font` в `main`.
   - Пренаредете `feature/add-about-page` в `feature/change-font`.

   ```bash
   git checkout main
   git rebase feature/change-font

   git checkout feature/add-about-page
   git rebase feature/change-font
   ```

5. **Merge Back**: Сложете всичко в `main` чрез rebase.
   ```bash
   git checkout main
   git rebase feature/add-about-page
   ```

## 7. Качване към централното хранилище

1. **Качване**: Качете вашите промени към централното хранилище.
   ```bash
    git push
    ```

2. Направете `pull request` към оригиналното хранилище, което сте fork-нали
