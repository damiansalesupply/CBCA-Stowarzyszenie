# END OF SESSION — Procedura zamknięcia sesji Claude

> Wykonaj te kroki **przed zakończeniem każdej sesji pracy** z Claude.  
> Dotyczy każdej osoby z zarządu: Damiana, Marcina, Macieja.

---

## ✅ Checklista końca sesji

### 1. Zapisz niezapisane zmiany

Sprawdź, czy wszystkie edytowane pliki są zapisane:

```
git status
```

Jeśli są zmiany — zrób commit:

```
git add <pliki które edytowałeś>
git commit -m "docs: opis zmian"
git push origin main
```

> ⚠️ Nie pushuj bez zatwierdzenia — przypomnij Claude, że wymaga Twojego OK.

---

### 2. Zaktualizuj bazę wiedzy (jeśli trzeba)

Jeśli w trakcie sesji pojawiły się **nowe informacje** o CBCA (nowy partner, nowa decyzja, zmiana cennika, nowy ekspert):

- Otwórz `CBCA_BAZA_WIEDZY.md`
- Dodaj/zaktualizuj odpowiednią sekcję
- Commit: `docs: aktualizacja bazy wiedzy — [temat]`

---

### 3. Notatka z sesji (opcjonalnie)

Jeśli sesja zawierała ważne ustalenia — poproś Claude o krótką notatkę:

> "Zrób notatkę z tej sesji — co zrobiliśmy, co zostało do zrobienia."

Claude zapisze ją jako plik `notes/SESSION_YYYYMMDD_[imię].md`.

---

### 4. Powiadom zespół (jeśli zmiana ich dotyczy)

Zasady komunikacji:
- **Zmiany w pakietach/cenach** → WhatsApp do Damiana + Marcina + Macieja
- **Zmiany w dokumentach prawnych** → WhatsApp do Damiana
- **Aktualizacje bazy wiedzy** → informacja na Discord #staff lub WhatsApp

---

### 5. Zamknij sesję

Powiedz Claude:

> "Zamknij sesję."

Claude potwierdzi, że wszystko jest zsynchronizowane.

---

## 📋 Format notatki z sesji

Claude tworzy plik `notes/SESSION_YYYYMMDD_[imię].md` w formacie:

```markdown
# Notatka z sesji — [Data] — [Imię]

## Co zrobiono
- punkt 1
- punkt 2

## Decyzje podjęte
- decyzja 1

## Do zrobienia (next session)
- zadanie 1
- zadanie 2

## Pliki zmienione
- CBCA_BAZA_WIEDZY.md — sekcja X
- Marketing - shared/...
```

---

## 🚫 Czego NIE robić na końcu sesji

- ❌ Nie pushuj zmian w plikach prawnych bez konsultacji z Damianem
- ❌ Nie usuwaj plików innych osób
- ❌ Nie zmieniaj struktury głównych folderów bez zgody 2 z 3 osób
- ❌ Nie commituj plików z hasłami (`.env`, tokeny, API keys)

---

## 🔄 Procedura dla Claude — "Zamknij sesję"

Gdy użytkownik powie "zamknij sesję" lub "end session", Claude wykonuje:

1. `git status` — sprawdza niezapisane zmiany
2. Jeśli są zmiany → pyta użytkownika czy commitować
3. Sugeruje commit message w formacie Conventional Commits
4. Po zatwierdzeniu → `git add`, `git commit`, `git push`
5. Potwierdza: "Sesja zamknięta. Repo zsynchronizowane."

---

*Ostatnia aktualizacja: 2026-05-22*
