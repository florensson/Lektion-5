# Testa merge-konflikt själv – Git i två branches (lokalt)

Denna övning visar hur du kan skapa och lösa en merge-konflikt lokalt genom att arbeta i två olika branches.

## Steg 1 – Initiera repo och första commit

```bash
git init konflikt-test
cd konflikt-test
echo 'Hej från start' > fil.txt
git add .
git commit -m "Första commit"
```

## Steg 2 – Skapa ny branch och ändra

```bash
git checkout -b branch-a
echo 'Ändrat i branch A' > fil.txt
git commit -am "Branch A ändring"
```

> OBS: Vi använder `-am` eftersom `fil.txt` redan är spårad (tracked). För nya filer krävs `git add` först.

## Steg 3 – Tillbaka till main och gör annan ändring

```bash
git checkout main
echo 'Ändrat i main' > fil.txt
git commit -am "Main ändring"
```

## Steg 4 – Försök slå ihop

```bash
git merge branch-a
```

Git upptäcker nu att `fil.txt` har ändrats i båda branches → **merge-konflikt**.

---

## Steg 5 – Lös konflikten

1. Öppna `fil.txt`  
2. Du ser något i stil med:

```text
<<<<<<< HEAD
Ändrat i main
=======
Ändrat i branch A
>>>>>>> branch-a
```

3. Ändra så som du vill att det ska se ut, t.ex:

```text
Ändrat i både main och branch A
```

4. Spara filen

---

## Steg 6 – Färdigställ mergandet

```bash
git add fil.txt     # eller git add .
git commit -m "Löst konflikt mellan main och branch-a"
```

---

Du har nu:
- skapat en konflikt
- löst den manuellt
- förstått hur Git spårar och slår ihop ändringar

Bra jobbat!
