# Lektion – Vecka 20: Git + API-intro

## Mål med lektionen

- Kunna samarbeta via Git och GitHub
- Förstå grundläggande Git-kommandon (`clone`, `commit`, `push`, `pull`)
- Förstå vad ett API är och kunna göra ett första API-anrop i PowerShell

---

## Git – Versionshantering i par

Ni ska jobba två och två. En av er skapar ett nytt GitHub-repo och bjuder in den andra som "Collaborator".

### Steg 1 – Klona repot

Båda klonar repot:

```bash
git clone https://github.com/ditt-användarnamn/ditt-repo.git
cd ditt-repo
```

### Steg 2 – Första commit och push

Skapa en enkel fil, t.ex. `hello.ps1`:

```powershell
Write-Host "Hej från $(whoami)"
```

Gör en commit och pusha:

```bash
git add hello.ps1
git commit -m "Första commit"
git push
```

### Steg 3 – Merge-konflikt (med flit)

- Båda ändrar samma rad i `hello.ps1`
- Båda gör `commit` och försöker `push`
- Den som pushar sist får en konflikt
- Lös konflikten manuellt:

```bash
git pull
# Redigera filen för att lösa konflikten
git add hello.ps1
git commit -m "Löst konflikt"
git push
```

---

## Vad är ett API?

API står för **Application Programming Interface**.  
Det är ett gränssnitt som låter våra skript prata med andra system, som webbtjänster.

Exempel: Vi kan fråga ett API om ett skämt, en kattfakta, eller väder – och få svaret som data.

De flesta API:er idag använder något som kallas för **REST**.

---

## Vad betyder `Invoke-RestMethod`?

PowerShell har ett kommando som heter `Invoke-RestMethod`.

| Del       | Förklaring                         |
|-----------|------------------------------------|
| `Invoke`  | Betyder "anropa" eller "köra"      |
| `REST`    | Är en stil för hur API:er byggs    |
| `Method`  | Vilken sorts anrop vi gör (t.ex. GET) |

Vi använder `GET`, som betyder att vi hämtar data.

**Så `Invoke-RestMethod` betyder:  
"Anropa ett REST-API och få tillbaka svaret som ett objekt i PowerShell."**

---

## Exempel: Öppet API utan nyckel

Vi börjar med ett öppet API som inte kräver någon nyckel eller inloggning.

### Cat Facts

```powershell
$response = Invoke-RestMethod "https://catfact.ninja/fact"
Write-Host "Kattfakta: $($response.fact)"
```

### Chuck Norris-joke

```powershell
$joke = Invoke-RestMethod "https://api.chucknorris.io/jokes/random"
Write-Host "Skämt: $($joke.value)"
```

---

OBS: Denna vecka fokuserar vi bara på öppna, nyckelfria API:er.  
Nästa vecka (vecka 21) lär vi oss om API:er som kräver autentisering via token.

---

## Övning – API i par

1. Skapa en ny fil i ert repo, t.ex. `api.ps1`
2. Välj ett öppet API (t.ex. de ovan)
3. Hämta data och skriv ut något från svaret

**Bonus:** Lägg in funktionen i en modulfil (`.psm1`)  
Exempel:

```powershell
function Get-RandomCatFact {
    $data = Invoke-RestMethod "https://catfact.ninja/fact"
    return $data.fact
}
```

Kalla sedan funktionen från ett skript:

```powershell
Import-Module ./Get-CatFacts.psm1
Write-Host (Get-RandomCatFact)
```

---

## Klar?

När ni är klara:

- Lägg till filerna i Git
- Skriv i `README.md`:
  - Vad ni testade
  - Hur det gick
  - Vem som gjorde vad
