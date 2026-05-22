# CBCA Stowarzyszenie — Zasady współpracy w repozytorium

> Repozytorium współdzielone przez 3 osoby z zarządu CBCA.  
> Każda osoba pracuje z własnym Claude (AI) jako asystentem.  
> Język wewnętrzny: PL | Język zewnętrzny (dokumenty publiczne): EN

---

## Zespół

| Osoba | Rola w CBCA | Obszar odpowiedzialności w repo |
|-------|------------|--------------------------------|
| **Damian Kuczyński** | Head of Operations, współzałożyciel | IT & technika, platforma Discord, onboarding |
| **Marcin Pondo** | Współzałożyciel, sprzedaż B2B | Sales, kontakty, market analysis |
| **Maciej Zagórowski** | Współzałożyciel, SEO/growth | Marketing, content, SEO, strona www |

---

## Zasady ogólne

### 1. Zanim zaczniesz pracę

```
git pull origin main
```

Zawsze synchronizuj repo przed edycją. Unikasz konfliktów.

### 2. Zakres zmian

- **Edytuj pliki ze swojego obszaru** (patrz tabela powyżej).
- Jeśli edytujesz plik innej osoby — zostaw komentarz w commicie dlaczego.
- Nie nadpisuj cudzej pracy bez konsultacji.

### 3. Commity — format

Używamy [Conventional Commits](https://www.conventionalcommits.org/):

```
docs: aktualizacja CBCA_BAZA_WIEDZY — nowe pakiety sponsorskie
feat: dodano szablon umowy z ekspertem
fix: poprawka budżetu Q2 2026
add: nowe loga w Marketing - shared/LOGA/
```

Krótki opis po dwukropku, po polsku lub angielsku — konsekwentnie.

### 4. Co wrzucamy do repo

✅ Dokumenty robocze (.md, .docx, .xlsx, .pdf)  
✅ Loga, materiały graficzne  
✅ Szablony, regulaminy, statuty  
✅ Notatki ze spotkań  
✅ Baza wiedzy (CBCA_BAZA_WIEDZY.md, CBCA_PROJECT_CONTEXT.md)  

❌ Pliki z hasłami lub dostępami (API keys, tokeny)  
❌ Pliki tymczasowe (.tmp, .DS_Store, Thumbs.db)  
❌ Pliki >50 MB (wrzuć na Drive zamiast)  

### 5. Konflikty

Jeśli pojawi się conflict git:
1. Nie force-pushuj (`git push --force` = zabronione)
2. Napisz na WhatsApp/Discord do pozostałych
3. Razem rozwiążcie conflict, potem push

---

## Praca z Claude (AI)

Każda osoba ma swojego Claude. Żeby Claude działał skutecznie w tym projekcie:

### Na początku każdej sesji Claude powinien:

1. Przeczytać `CBCA_PROJECT_CONTEXT.md` — kontekst organizacji
2. Przeczytać `CBCA_BAZA_WIEDZY.md` — wiedza o CBCA
3. Sprawdzić `END_OF_SESSION.md` — procedura zamykania sesji
4. Zrobić `git pull` żeby mieć aktualny stan repo

### Claude może:

- Edytować pliki dokumentacyjne i bazę wiedzy
- Tworzyć nowe pliki w odpowiednich folderach
- Robić commity i pushe po zatwierdzeniu przez użytkownika
- Wrzucać pliki na Google Drive przez MCP
- Tworzyć PDF-y i inne materiały

### Claude nie może bez zapytania:

- Usuwać cudzych plików
- Zmieniać struktury folderów głównych
- Pushować zmian do repo bez potwierdzenia użytkownika
- Edytować plików prawnych (Legal - Contracts/) — tylko czytać

---

## Struktura folderów

```
CBCA-Stowarzyszenie/
│
├── 📄 README.md                    — opis projektu Discord (IT)
├── 📄 CBCA_PROJECT_CONTEXT.md      — GŁÓWNY KONTEKST dla Claude i zespołu
├── 📄 CBCA_BAZA_WIEDZY.md          — baza wiedzy organizacji
├── 📄 RULES.md                     — ten plik
├── 📄 END_OF_SESSION.md            — procedura zamknięcia sesji
│
├── 📁 Legal - Contracts/           — dokumenty prawne [Damian]
│   ├── Do Podpisu - założycielskie/
│   └── Ekspert dokumenty/
│
├── 📁 Marketing - shared/          — materiały marketingowe [Maciej]
│   └── LOGA/
│
├── 📁 Marcin files/                — pliki Marcina [Marcin]
│   └── Wiedza/
│
├── 📁 Establishment files/         — dokumenty założycielskie [Damian]
│
├── 📁 Website Materials/           — strona www [Maciej]
│
└── 📄 [inne pliki robocze]
```

---

## Decyzje i komunikacja

- **Zmiany w dokumentach prawnych** → konsultacja z Damianem przed pushem
- **Zmiany w pakietach/cenach** → konsultacja całego zarządu (3 osoby)
- **Aktualizacje bazy wiedzy** → każdy może, ale informuje pozostałych
- **Nowe foldery** → zgoda 2 z 3 osób

**Kanał komunikacji wewnętrznej:** WhatsApp / Discord CBCA Staff

---

*Ostatnia aktualizacja: 2026-05-22*
