# Отмяна на промени

Това упражнение ще научите как отменяте промени, които сте направили във вашият проект. За целта ще използвате командите:

- `git commit --amend`
- `git reset`
- `git restore`

## Инициализация

1. Инициализирайте ново празно хранилище в GitHub
2. Клонирайте вашето хранилище

```bash
git clone <вашето-хранилище>
cd <вашето-хранилище>
```

3.  Добавете тестов файл и го запишете

```bash
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit"
```

## Отмяна на запис с `git commit --amend`

1. Направете промяна и я запишете

```bash
echo "Some changes" >> file.txt
git add file.txt
git commit -m "Add some changes"
```

2. Опа! Забравихте да направите още една промяна. Добавете я към файла `file.txt`

```bash
echo "Forgotten change" >> file.txt
```

3. Променете последният запис да включва тази промяна

```bash
git add file.txt
git commit --amend -m "Add some changes and forgotten change"
```

4. Потвърдете промяната. Изпълнете командата `git log`, за да потвърдите че съобщението на последният запис се е променила и двете промени са добавени

## Отменяне на staged промени и записи чрез `git reset`

1. Направете още една промяна и я запишете

```bash
echo "Another change" >> file.txt
git add file.txt
git commit -m "Add another change"
```

2. Отменете последният запис, като запазвате промените в работната директория

```bash
git reset HEAD~1
```

3. Отменете последният запис напълно, включително промените в работната директория

```bash
git reset --hard HEAD~1
```


## Отменяне на промени в работещата директория чрез `git restore`

1. Направете промяна без да я добавяте към staging area

```bash
echo "Unwanted change" >> file.txt
```

2. Отменете промяната

```bash
git restore file.txt
```

3. Направете промяна и я добавете към staging area

```bash
echo "Staged change" >> file.txt
git add file.txt
```

4. Отменете промяната

```bash
git restore --staged file.txt
```
