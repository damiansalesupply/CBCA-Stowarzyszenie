# CBCA Discord — Pełny opis projektu

> **Stan na:** 2026-05-07  
> **Projekt:** Cross Border Commerce Association — platforma Discord + panel admina + onboarding  
> **Zarządzanie IT:** Damian Kuczkowski (GitHub: [@damiansalesupply](https://github.com/damiansalesupply)) — właściciel projektu i główny deweloper  
> **Repozytorium:** https://github.com/damiansalesupply/discord-community-ops *(private)*

---

## Spis treści

1. [Co to jest CBCA Discord](#1-co-to-jest-cbca-discord)
2. [Adresy i linki](#2-adresy-i-linki)
3. [Platforma onboardingowa — formularz /apply](#3-platforma-onboardingowa--formularz-apply)
4. [Panel admina — opis i wszystkie sekcje](#4-panel-admina--opis-i-wszystkie-sekcje)
5. [Boty Discord — role i funkcje](#5-boty-discord--role-i-funkcje)
6. [Role na serwerze Discord](#6-role-na-serwerze-discord)
7. [Kanały Discord](#7-kanały-discord)
8. [Przepływy funkcjonalne](#8-przepływy-funkcjonalne)
9. [Stack techniczny i infrastruktura](#9-stack-techniczny-i-infrastruktura)
10. [Jak zarządzać projektem IT](#10-jak-zarządzać-projektem-it)

---

## 1. Co to jest CBCA Discord

**Cross Border Commerce Association** to zamknięta społeczność dla właścicieli sklepów e-commerce, ekspertów branżowych i dostawców usług. Platforma opiera się na Discord jako głównym miejscu wymiany wiedzy, networkingu i moderacji.

System składa się z trzech warstw:

- **Discord** — serwer z kanałami, rolami, 6 botami AI
- **Strona /apply** — publiczny formularz aplikacyjny dla nowych członków
- **Panel admina** — prywatny panel do zarządzania całą platformą (aplikacje, moderacja, baza wiedzy, boty, ustawienia)

Wszystko działa automatycznie: od momentu złożenia aplikacji przez kandydata, przez zatwierdzenie przez admina jednym kliknięciem, aż po automatyczne przypisanie roli na Discord i wiadomość powitalną — bez żadnych ręcznych kroków poza decyzją admina.

---

## 2. Adresy i linki

| Co | URL | Dostęp |
|----|-----|--------|
| **Formularz aplikacyjny** | https://app.cross-border-association.com/apply | Publiczny — dla każdego |
| **Panel admina** | https://app.cross-border-association.com | Tylko Admin — logowanie przez Discord OAuth |
| **Dashboard** | https://app.cross-border-association.com/dashboard | Admin |
| **Aplikacje (zatwierdzanie)** | https://app.cross-border-association.com/dashboard/applications | Admin |
| **Edytor formularza /apply** | https://app.cross-border-association.com/dashboard/applications | Admin (zakładka Form editor) |
| **Edytor emaili** | https://app.cross-border-association.com/dashboard/applications | Admin (zakładka Email templates) |
| **Forum Guard (słowa kluczowe)** | https://app.cross-border-association.com/dashboard/forum-guard | Admin |
| **Ustawienia platformy** | https://app.cross-border-association.com/dashboard/settings | Admin |
| **Konfiguracja SMTP** | https://app.cross-border-association.com/dashboard/settings/smtp | Admin |
| **Alerty** | https://app.cross-border-association.com/dashboard/alerts | Admin |
| **Mapowania ról/kanałów** | https://app.cross-border-association.com/dashboard/mappings | Admin |
| **Baza wiedzy** | https://app.cross-border-association.com/dashboard/knowledge | Admin |
| **Dokumentacja bot** | https://app.cross-border-association.com/dashboard/documentation | Admin |
| **Prompty LLM** | https://app.cross-border-association.com/dashboard/prompts | Admin |
| **Log audytu** | https://app.cross-border-association.com/dashboard/audit | Admin |
| **Dokumentacja wbudowana** | https://app.cross-border-association.com/dashboard/help | Admin |

---

## 3. Platforma onboardingowa — formularz /apply

### Link dla kandydatów

```
https://app.cross-border-association.com/apply
```

Formularz jest **całkowicie publiczny** — nie wymaga żadnego logowania. Kandydat wchodzi, wypełnia 4 kroki i wysyła aplikację.

### Jak wygląda formularz (4 kroki)

1. **Wybór roli** — kandydat wybiera kim jest:
   - 🏪 **Owner / Member** — właściciel sklepu e-commerce (core membership)
   - 🎓 **Expert** — ekspert branżowy (SEO, logistyka, prawo, marketing, etc.)
   - 🛠️ **Service Provider** — dostawca usług dla e-commerce

2. **Dane podstawowe** — imię, nazwisko, email, firma

3. **Szczegóły** — pytania specyficzne dla wybranej roli (np. URL sklepu, specjalizacja, opis usług)

4. **Podgląd i wysyłka** — kandydat widzi podsumowanie i zatwierdza

Po wysłaniu kandydat dostaje **email potwierdzający** z informacją, że aplikacja jest w trakcie rozpatrywania.

### Jak edytować formularz

Wszystkie elementy formularza są **edytowalne z poziomu panelu admina** — bez zmian w kodzie:

**Pola formularza:**
→ Panel → **Applications** → zakładka **Form editor**  
→ Można zmieniać kolejność pytań, treść, opcje odpowiedzi, wymagalność, przypisanie do roli  
→ URL: https://app.cross-border-association.com/dashboard/applications

**Treść emaili transakcyjnych (3 szablony):**
→ Panel → **Applications** → zakładka **Email templates**  
→ Edytowalne szablony:
- Email potwierdzający (wysyłany natychmiast po złożeniu aplikacji)
- Email z zaproszeniem (wysyłany po zatwierdzeniu przez admina — zawiera jednorazowy link Discord)
- Email z odmową (wysyłany po odrzuceniu)
→ Szablony obsługują markdown + zmienne dynamiczne (np. imię kandydata, rola, link invite)

**Ustawienia globalne onboardingu:**
→ Panel → **Settings**  
→ Np. czas ważności invite (domyślnie 7 dni), max użycia invite, tekst powitalny DM

### Pełny flow onboardingu krok po kroku

```
1. Kandydat wchodzi na /apply
         ↓
2. Wypełnia 4-krokowy formularz i wysyła
         ↓
3. System wysyła email potwierdzający (automatycznie)
         ↓
4. Na kanale #applications-review pojawia się embed Discord
   z danymi kandydata + przyciskami reakcji:
   ✅ Zatwierdź  |  ❌ Odrzuć
         ↓
5a. Admin klika ✅
    → System generuje jednorazowy link invite Discord
      (max 1 użycie, ważny 7 dni)
    → Wysyła email z linkiem i instrukcją dołączenia
         ↓
    Kandydat klika link → dołącza do Discorda
         ↓
    Bot dcops-gateway wykrywa nowego członka
    → mapuje invite → przypisuje rolę Discord (Owner/Expert/Provider)
    → wysyła spersonalizowany DM powitalny (napisany przez LLM)
         ↓
    Bot dcops-alerts publikuje post na #welcome

5b. Admin klika ❌
    → System wysyła email z odmową
    → Aplikacja zamknięta
```

---

## 4. Panel admina — opis i wszystkie sekcje

**Adres:** https://app.cross-border-association.com  
**Logowanie:** Kliknij „Sign in with Discord" → autoryzacja OAuth → system weryfikuje czy konto ma rolę Admin w bazie danych

> Jeśli konto nie ma roli Admin w DB — dostęp odrzucony nawet przy poprawnym logowaniu Discord. Nowych adminów dodaje Damian bezpośrednio w bazie.

### Wszystkie sekcje panelu (15)

| Sekcja | URL | Co można zrobić |
|--------|-----|-----------------|
| **Dashboard** | /dashboard | Przegląd aktywności: liczba aplikacji, alertów, moderacji |
| **Applications** | /dashboard/applications | Lista wszystkich aplikacji (filtrowanie, status), zatwierdzanie/odrzucanie, export XLSX, **edytor formularza /apply**, **edytor szablonów emaili** |
| **Forum Guard** | /dashboard/forum-guard | Edycja listy słów kluczowych (PL i EN), wzorców regex, progu score (0–1); przycisk **Test klasyfikatora** — wklej tekst i sprawdź co bot z nim zrobi |
| **Moderation** | /dashboard/moderation | Kolejka przypadków moderacyjnych wykrytych przez Forum Guard (przegląd, zamykanie) |
| **Reports** | /dashboard/reports | Zgłoszenia od użytkowników przez komendę Discord `/report` |
| **Knowledge** | /dashboard/knowledge | Baza wiedzy wyłuskanej z wątków forum (zaaprobowane przez ✅ na #knowledge-review) |
| **Documentation** | /dashboard/documentation | Baza dokumentacji wgranej przez kanał #documentation_bot |
| **Prompts** | /dashboard/prompts | Edycja 11 promptów LLM używanych przez boty + przycisk **Test na żywo** (wyślij prompt, zobaczysz odpowiedź modelu) |
| **Alerts** | /dashboard/alerts | Tworzenie i edycja reguł alertów (typ triggera, kanał Discord, rola odbiorcy, quiet hours); zakładka **Log** — historia dostarczonych alertów |
| **Settings** | /dashboard/settings | 31 ustawień skalarnych: progi similarności RAG, minimalna liczba odpowiedzi do analizy wątku, limity, flagi funkcji |
| **SMTP** | /dashboard/settings/smtp | Konfiguracja serwera email: host, port, login, hasło (szyfrowane AES-256-GCM w DB), test wysyłki |
| **Mappings** | /dashboard/mappings | Mapowania ról Discord (nazwa → ID) i kanałów Discord (nazwa → ID) — wymagane do poprawnego działania botów |
| **Audit** | /dashboard/audit | Pełny log wszystkich zdarzeń systemowych z timestampami i autorami |
| **Flows** | /dashboard/flows | Diagramy Mermaid wizualizujące logikę botów — przydatne do onboardingu nowych adminów |
| **Help** | /dashboard/help | Wbudowana dokumentacja admina (940 linii), przeszukiwalna, z opisem każdej funkcji |

---

## 5. Boty Discord — role i funkcje

Na serwerze CBCA działa **6 botów Discord**. Każdy pełni inną rolę i jest osobnym procesem (osobny kontener Docker).

---

### Bot 1 — dcops-gateway
**ID:** 1497999767391961262  
**Rola:** Centralny event broker

Nasłuchuje **wszystkich zdarzeń** na serwerze Discord:
- Nowe posty na forum → enqueue zadania do analizy
- Nowi członkowie → wykrywanie przez które zaproszenie dołączyli (invite tracking)
- Komendy slash: `/report` (zgłoszenie treści) i `/flag-post` (ręczne oznaczenie)

Bez tego bota reszta systemu nie działa — to on zbiera dane i przekazuje do kolejek.

> ⚠️ **Wymaga uprawnień:** Manage Server — bez tego nie widzi listy zaproszeń i invite tracking nie działa.

---

### Bot 2 — dcops-forum-guard
**ID:** 1498005023265914881  
**Rola:** Automatyczny moderator forum

Każdy post na forum przechodzi przez dwa etapy analizy:

1. **Regex** — sprawdzenie słów kluczowych PL/EN, wzorców cenowych (`99 zł`, `promocja`, `kup teraz`), emoji sprzedażowych → wynik 0–1
2. **LLM (Anthropic Claude Haiku)** — dla wyników 0,3–0,7 (niejednoznacznych) → klasyfikacja: `clean` / `suspicious` / `likely_sales`

Wynik `suspicious` lub `likely_sales` → tworzy ModerationCase + alert na kanale #mod-alerts.

Słowa kluczowe, regex i próg są **edytowalne w panelu** → `/dashboard/forum-guard`.

---

### Bot 3 — dcops-alerts
**ID:** 1498006143983681727  
**Rola:** Powiadomienia + Welcome + Zatwierdzanie aplikacji

Trzy funkcje w jednym:

**Alerty** — dostarczanie powiadomień moderacyjnych:
- Filtrowanie przez LLM (czy warto wysłać?)
- Quiet hours Europe/Warsaw (nie budzi moderatorów w nocy)
- Deduplikacja przez Redis (ten sam trigger nie generuje 10 alertów)
- Dostarcza na kanały Discord lub DM do konkretnych ról

**Welcome** — po dołączeniu nowego członka przez invite:
- Pobiera dane z aplikacji
- Generuje spersonalizowany DM powitalny (przez LLM)
- Publikuje post na kanale #welcome

**Zatwierdzanie aplikacji** — obsługuje reakcje ✅/❌ na kanale #applications-review

> ⚠️ **Wymaga:** rola `dcops-alerts` musi być **wyżej w hierarchii** niż wszystkie role użytkowników — Discord blokuje botowi nadawanie ról równych lub wyższych sobie.

---

### Bot 4 — dcops-knowledge
**ID:** 1498007455232299059  
**Rola:** Bot Q&A + zarządzanie bazą wiedzy

**Q&A:** Odpowiada na pytania zadane przez @mention lub `/ask`:
- Generuje embedding pytania (OpenAI text-embedding-3-small)
- Cosine similarity → top-3 najbardziej pasujące fragmenty z bazy wiedzy
- Próg: 0,35 — poniżej bot odpowiada „nie wiem"
- Claude Haiku generuje odpowiedź na podstawie kontekstu

**Zarządzanie KB:**
- Obsługuje reakcje na kanale #knowledge-review: ✅ (dodaj do KB) / ❌ (odrzuć) / ✏️ (edytuj)
- Obsługuje reakcje na kanale #applications-review (dla bota dcops-alerts)

---

### Bot 5 — dcops-documentation
**ID:** 1498009908853866538  
**Rola:** Bot dokumentacyjny

Obsługuje kanał **#documentation_bot**:
- Właściciel kanału wgrywa post lub plik `.md` / `.txt`
- Bot automatycznie dzieli dokument na chunki (po nagłówkach H2, sliding window 3000+150 znaków dla dłuższych)
- Generuje embeddingi i zapisuje w bazie wiedzy (kbType=documentation)

Dostępny dla użytkowników przez:
- `@dcops-documentation pytanie` — odpowiedź z kontekstem z dokumentacji
- `/ask pytanie` — to samo przez komendę slash

---

### Bot 6 — dcops-web-login
**Rola:** OAuth dla panelu admina

Nie jest widoczny na serwerze Discord. Służy wyłącznie do obsługi logowania przez Discord OAuth 2.0 do panelu administracyjnego. Weryfikuje uprawnienia (rola Admin w DB) i zarządza sesją.

---

## 6. Role na serwerze Discord

### Role użytkowników

| Rola | Kto ma | Dostęp |
|------|--------|--------|
| **Admin** | Administratorzy platformy | Wszystkie kanały + panel admina na stronie |
| **Owner / Member** | Właściciele sklepów e-commerce | Forum #owners-questions, kanały COMMUNITY |
| **Expert** | Eksperci branżowi | Forum #expert-questions, kanały COMMUNITY |
| **Service Provider** | Dostawcy usług dla e-commerce | #provider-intros, #provider-offers, kanały COMMUNITY |

Role są **automatycznie przypisywane** po zatwierdzeniu aplikacji i dołączeniu przez invite — na podstawie wyboru z kroku 1 formularza /apply. Admin nie musi ręcznie nadawać ról.

### Role botów (techniczne)

| Rola | Bot | Krytyczne uprawnienia |
|------|-----|-----------------------|
| dcops-gateway | Bot 1 | **Manage Server** (wymagane do invite tracking!) |
| dcops-forum-guard | Bot 2 | Manage Roles, Manage Channels |
| dcops-alerts | Bot 3 | **Create Invite + Manage Roles** — rola WYŻEJ niż user roles! |
| dcops-knowledge | Bot 4 | Odczyt kanałów #knowledge-review, #applications-review |
| dcops-documentation | Bot 5 | Odczyt #documentation_bot |
| dcops-web-login | Bot 6 | Brak widoczności na serwerze (tylko OAuth) |

> **Ważne:** Hierarchia ról botów w Discord musi być zachowana. dcops-alerts musi być wyżej w hierarchii niż Owner, Expert i Service Provider — inaczej nie może nadawać tych ról nowym członkom.

---

## 7. Kanały Discord

### Struktura kanałów

```
📋 INFO
  #regulamin           — Zasady serwera (tylko odczyt)

🌍 COMMUNITY
  #welcome             — Powitania nowych członków (generowane automatycznie przez bota)
  #owners-questions    — Forum pytań dla właścicieli sklepów [Owner/Member + Expert + Admin]
  #expert-questions    — Forum pytań eksperckich [Expert + Admin]
  #help                — Ogólna pomoc [wszyscy]

🛠️ PROVIDERS
  #provider-intros     — Prezentacje dostawców usług [Service Provider + Admin]
  #provider-offers     — Oferty dostawców [Service Provider + Admin]

🔒 STAFF (tylko Admin i boty)
  #mod-alerts          — Alerty moderacyjne od Forum Guard i innych triggerów
  #knowledge-review    — Kandydaci do bazy wiedzy — Admin ocenia ✅/❌/✏️
  #applications-review — Aplikacje do zatwierdzenia — Admin ocenia ✅/❌
  #bot-logs            — Logi techniczne botów
  #ops                 — Operacje serwera
  #documentation_bot   — Upload dokumentacji + Q&A z dcops-documentation
```

### Który bot działa na którym kanale

| Kanał | Bot |
|-------|-----|
| #welcome | dcops-alerts (publikuje powitanie) |
| #owners-questions, #expert-questions | dcops-gateway (zbiera posty do analizy) |
| #mod-alerts | dcops-alerts (dostarcza alerty) |
| #knowledge-review | dcops-knowledge (obsługuje reakcje ✅/❌/✏️) |
| #applications-review | dcops-knowledge + dcops-alerts (embed + reakcje) |
| #documentation_bot | dcops-documentation (ingest + Q&A) |

---

## 8. Przepływy funkcjonalne

### 8.1 Onboarding nowego członka

Opisany szczegółowo w [sekcji 3](#3-platforma-onboardingowa--formularz-apply).

### 8.2 Forum Guard — moderacja sprzedażowa

```
Użytkownik publikuje post na forum
        ↓
dcops-gateway wykrywa → enqueue "classify-post"
        ↓
dcops-forum-guard:
  → krok 1: analiza regex (słowa kluczowe PL+EN, ceny, emoji) → score 0–1
  → krok 2 (jeśli 0.3–0.7): LLM (Claude Haiku) → clean | suspicious | likely_sales
        ↓
suspicious / likely_sales:
  → tworzy ModerationCase w DB
  → dcops-alerts wysyła alert na #mod-alerts
```

### 8.3 Knowledge Curate — forum → baza wiedzy

```
Wątek forum osiąga minimalną liczbę odpowiedzi (konfig. w Settings)
        ↓
dcops-gateway → enqueue "evaluate-thread"
        ↓
LLM ocenia: czy wątek zawiera wartościową wiedzę? → {worthy, reason, topic}
        ↓
Jeśli worthy:
  → LLM tworzy draft: {title, body, tags}
  → Embed na #knowledge-review
        ↓
Admin klika ✅ → KnowledgeEntry + embedding OpenAI → dostępne w RAG
Admin klika ❌ → odrzucone
Admin klika ✏️ → edycja draftu przed zatwierdzeniem
```

### 8.4 Documentation Bot — wgrywanie wiedzy

```
Admin/właściciel wgrywa post lub plik .md na #documentation_bot
        ↓
dcops-documentation:
  → auto-chunking (split po nagłówkach ## H2)
  → sliding window 3000+150 znaków dla dłuższych sekcji
  → embedding OpenAI per chunk
  → zapis do DB (kbType=documentation)
        ↓
Użytkownik: @dcops-documentation pytanie lub /ask pytanie
  → cosine similarity → top-3 chunki (próg 0.35)
  → Claude Haiku generuje odpowiedź z kontekstem
```

### 8.5 Alerty

```
Trigger: sales_flag | unanswered_question | report_created
        ↓
Sprawdzenie reguły AlertRule (enabled? triggerType pasuje?)
        ↓
Deduplikacja Redis (SET NX EX) — ten sam trigger przez X minut = tylko 1 alert
        ↓
Quiet hours check (Europe/Warsaw) — nocna cisza
        ↓
LLM filter → {send: true/false, severity, reason}
        ↓
LLM format → tekst powiadomienia
        ↓
Delivery: kanał Discord + DM do użytkowników z daną rolą
```

---

## 9. Stack techniczny i infrastruktura

### Serwer

| Parametr | Wartość |
|----------|---------|
| VPS | Hetzner Cloud, IP: 62.238.2.26 |
| System | Ubuntu 24.04 |
| Docker | 29.4.1 |
| Liczba kontenerów | 12 |
| Reverse proxy | Caddy (auto SSL/TLS przez Let's Encrypt) |
| Domena | cross-border-association.com (DNS: Cyberfolks) |

### Technologie

| Warstwa | Technologia |
|---------|-------------|
| **Backend API** | NestJS (Node.js) |
| **Boty Discord** | discord.js v14 (każdy bot = osobny serwis) |
| **Kolejki zadań** | BullMQ + Redis 7 |
| **Frontend (panel)** | Next.js 14 + NextAuth v4 |
| **Baza danych** | PostgreSQL 16 + Prisma ORM |
| **Storage plików** | MinIO (S3-compatible) |
| **AI — generowanie** | Anthropic Claude Haiku 4.5 |
| **AI — embeddingi** | OpenAI text-embedding-3-small |
| **Email** | SMTP Cyberfolks, port 587 STARTTLS, DKIM włączony |

### Kontenery Docker (12)

```
web-admin          → panel admina Next.js (port 3000, Caddy → HTTPS)
api-core           → NestJS backend
discord-gateway    → bot dcops-gateway
forum-guard-worker → bot dcops-forum-guard + worker
alerts-worker      → bot dcops-alerts + worker
knowledge-worker   → worker dla bazy wiedzy
knowledge-bot      → bot dcops-knowledge (Q&A Discord)
documentation-bot  → bot dcops-documentation
db                 → PostgreSQL 16
redis              → Redis 7
minio              → MinIO storage
caddy              → reverse proxy + SSL
```

---

## 10. Jak zarządzać projektem IT

### Kto zarządza

**Damian Kuczkowski** — właściciel projektu i główny deweloper  
GitHub: [@damiansalesupply](https://github.com/damiansalesupply)  
Repozytorium: https://github.com/damiansalesupply/discord-community-ops *(private)*

Projekt jest rozwijany przy pomocy **Claude Code (AI)** — asystenta programistycznego. Większość kodu i konfiguracji powstała we współpracy człowiek-AI.

### Gdzie jest kod

```
Lokalnie:  C:\projects\discord-community-ops
VPS:       /home/claude-agent/discord-community-ops
GitHub:    https://github.com/damiansalesupply/discord-community-ops
```

### Jak wdrażać zmiany (uproszczony flow)

```bash
# 1. Zmiana kodu lokalnie

# 2. Push do GitHub
git add .
git commit -m "opis zmiany"
git push

# 3. Na VPS — aktualizacja
ssh claude-agent@62.238.2.26
cd /home/claude-agent/discord-community-ops
git pull

# 4. Rebuild i restart serwisu
docker compose build <nazwa-serwisu>
docker compose up -d --force-recreate <nazwa-serwisu>

# 5. Sprawdź logi
docker compose logs -f <nazwa-serwisu>
```

### Co można zmienić BEZ dotykania kodu (tylko przez panel)

- ✅ Treść formularza /apply (pytania, opcje)
- ✅ Szablony emaili (potwierdzenie, zaproszenie, odmowa)
- ✅ Słowa kluczowe Forum Guard (lista PL+EN, regex, próg)
- ✅ Prompty LLM (11 promptów, edytor + test na żywo)
- ✅ Reguły alertów (typy triggerów, kanały, quiet hours)
- ✅ 31 ustawień skalarnych platformy
- ✅ Konfiguracja SMTP
- ✅ Mapowania ról i kanałów Discord

### Co wymaga zmiany kodu (deploy)

- ❌ Nowe funkcje botów
- ❌ Nowe pola w bazie danych (migracja Prisma)
- ❌ Nowe kanały Discord wymagające nowej logiki
- ❌ Zmiana modelu AI lub providera

### Dostęp awaryjny

Jeśli panel admina nie działa, można zarządzać bezpośrednio przez SSH:

```bash
ssh -i ~/.ssh/id_ed25519_vps claude-agent@62.238.2.26

# Stan wszystkich kontenerów
cd /home/claude-agent/discord-community-ops
docker compose ps

# Restart konkretnego serwisu
docker compose restart knowledge-bot

# Logi na żywo
docker compose logs -f web-admin
```

---

*Dokument wygenerowany na podstawie kodu źródłowego i dokumentacji projektu discord-community-ops.*  
*Ostatnia aktualizacja: 2026-05-07*
