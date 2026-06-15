# polyGo — Sygnały: Specyfikacja funkcji
> **Dokument:** sygnaly-feature-spec | **Wersja:** 1 | **Data:** czerwiec 2026
> **Zakres:** pełna specyfikacja funkcji Sygnały — v2 platformy polyGo
> **Status:** Do zatwierdzenia

---

## Spis treści
1. [Cel i kontekst](#1-cel-i-kontekst)
2. [Terminologia](#2-terminologia)
3. [Role i uprawnienia](#3-role-i-uprawnienia)
4. [Typy sygnałów](#4-typy-sygnałów)
5. [Struktura sygnału — pola wspólne](#5-struktura-sygnału--pola-wspólne)
6. [Struktura sygnału — pola branżowe](#6-struktura-sygnału--pola-branżowe)
7. [Dystrybucja — mechanizm "kto widzi"](#7-dystrybucja--mechanizm-kto-widzi)
8. [Feed — widok agregowany](#8-feed--widok-agregowany)
9. [Cykl życia sygnału](#9-cykl-życia-sygnału)
10. [Powiadomienia push i alerty](#10-powiadomienia-push-i-alerty)
11. [Powiązania z innymi modułami](#11-powiązania-z-innymi-modułami)
12. [Kluczowe przepływy UX](#12-kluczowe-przepływy-ux)
13. [Decyzje produktowe](#13-decyzje-produktowe)
14. [Poza zakresem v2](#14-poza-zakresem-v2)
15. [Otwarte pytania](#15-otwarte-pytania)

---

## 1. Cel i kontekst

### Czym są Sygnały

Sygnały to system rynkowych komunikatów wewnątrz zamkniętej sieci polyGo. Firma publikuje **sygnał podaży** (mamy coś do sprzedania/oddania) lub **sygnał popytu** (szukamy czegoś do kupienia/pozyskania) i kontroluje, kto go widzi. Inne firmy reagują przez wbudowany komunikator.

Sygnały **nie są** marketplace'em:
- Brak cennika, brak transakcji, brak escrow
- Brak publicznych listingów dostępnych bez logowania
- Brak mechanizmu aukcyjnego
- Cała rozmowa handlowa toczy się przez komunikator polyGo

Sygnały **są** mechanizmem kontrolowanego rozgłaszania:
- Świeżość jest strukturalna — sygnał podaży powiązany ze stanem magazynu wygasa automatycznie
- Dystrybucja jest intencjonalna — nadawca decyduje kto widzi sygnał
- Odpowiedź jest natychmiastowa — jeden klik otwiera rozmowę z kontekstem sygnału

### Dlaczego v2, nie MVP

Funkcja jest wartościowa wyłącznie przy odpowiedniej liczbie aktywnych firm. Feed z 20-40 firmami wygląda martwo i buduje złe pierwsze wrażenie. Próg uruchomienia, przy którym feed generuje wartość, szacowany jest na ~80 aktywnych zweryfikowanych firm. MVP skupia się na rdzeniu: znajdź firmę → napisz do niej. Sygnały są pierwszą dużą funkcją v2 — budowaną na zweryfikowanej sieci.

### Trigger uruchomienia

Wdrożenie Sygnałów zalecane po osiągnięciu 80+ aktywnych firm na platformie.

---

## 2. Terminologia

| Termin | Definicja |
|--------|-----------|
| **Sygnał** | Jeden komunikat rynkowy (podaży lub popytu) opublikowany przez firmę |
| **MAMY** | Sygnał podaży — firma informuje, że posiada coś dostępnego |
| **SZUKAMY** | Sygnał popytu — firma informuje, że czegoś potrzebuje / szuka |
| **Nadawca** | Firma publikująca sygnał |
| **Odbiorca** | Firma/użytkownik widzący sygnał w feedzie lub przez powiadomienie |
| **Feed** | Agregowany, chronologiczny widok sygnałów od wielu firm |
| **Alert** | Subskrypcja użytkownika na sygnały spełniające określone kryteria |
| **Dystrybucja** | Ustawienie określające kto widzi dany sygnał |
| **Segment** | Nazwana lista kontaktów stworzona przez firmę (np. "Klienci HDPE") |
| **Ważność sygnału** | Okres przez który sygnał jest aktywny i widoczny |

---

## 3. Role i uprawnienia

| Akcja | Admin polyGo | Company Owner/Admin | Employee |
|-------|-------------|---------------------|----------|
| Tworzenie sygnału | — | TAK | TAK |
| Edycja własnego sygnału | — | TAK | TAK (tylko swoje) |
| Usunięcie sygnału firmy | — | TAK | TAK (tylko swoje) |
| Przeglądanie feedu | — | TAK | TAK |
| Ustawianie alertów | — | TAK | TAK |
| Obserwowanie firm | — | TAK | TAK |
| Moderacja sygnałów (ukrycie/usunięcie) | TAK | — | — |
| Podgląd statystyk sygnałów | — | TAK | NIE |

> **Zasada:** Sygnał jest publikowany w imieniu firmy, nie pracownika. Na sygnale widnieje nazwa firmy i kategoria branżowa. Imię pracownika, który go stworzył, jest widoczne wyłącznie dla Owner/Admin tej firmy (do celów wewnętrznych).

---

## 4. Typy sygnałów

### 4.1 MAMY — sygnał podaży

Firma informuje, że posiada coś dostępnego teraz lub w określonym terminie.

Przykłady:
- Recykler: 24t HDPE PCR regranulat, food-contact, dostępne od zaraz
- Producent: wolne moce wtryskowe — 3 okna produkcyjne w lipcu
- Trader: partia off-spec PP-Homo, 8t, cena negocjowalna
- Maszyny: używana wtryskarka Engel 250t, 2018, stan dobry

### 4.2 SZUKAMY — sygnał popytu

Firma informuje, że czegoś szuka lub potrzebuje.

Przykłady:
- Recykler: potrzebujemy 60t HDPE PCR odpad komunalny/PIR miesięcznie
- Producent: szukamy dostawcy PP-GF30 automotive, kontrakt roczny
- Broker: klient szuka 40t PE-LD folia transparentna (anonimowo)
- Laboratorium: zlecę jednorazowe badania FTIR + DSC — pilne, 3 próbki

---

## 5. Struktura sygnału — pola wspólne

Pola wypełniane przy każdym sygnale, niezależnie od branży.

### Pola obowiązkowe

**Typ sygnału**
- Wartości: `MAMY` / `SZUKAMY`
- Widoczny jako kolorowy badge (np. zielony MAMY, niebieski SZUKAMY)

**Kategoria sygnału**
- Auto-wypełniana z kategorii branżowych firmy
- Jeśli firma ma kilka kategorii — nadawca wybiera jedną dla tego sygnału
- Wpływa na filtry feedu

**Tytuł**
- Typ: tekst jednoliniowy, max 80 znaków
- Propozycja auto-generowania na podstawie wypełnionych pól (edytowalna)
- Przykład auto: "MAMY: 24t HDPE PCR regranulat — dostępne od zaraz"

**Dystrybucja**
- Kto widzi ten sygnał (patrz sekcja 7)

### Pola opcjonalne (wspólne)

**Opis**
- Typ: tekst wieloliniowy, max 400 znaków
- Przeznaczenie: doprecyzowanie warunków, specyfikacja techniczna, uwagi logistyczne

**Ważność sygnału**
- Opcje:
  - `Do wyczerpania` — sygnał aktywny do ręcznego zamknięcia lub auto-wygaśnięcia
  - `Data wygaśnięcia` — użytkownik podaje datę (datepicker)
  - `Powiązany z magazynem` — tylko dla sygnałów MAMY z modułem magazynowym (v3+)
- Domyślnie: 30 dni z przypomnieniem o odnowieniu na 3 dni przed wygaśnięciem

**Pilność**
- Opcje: `brak` / `pilne (do 7 dni)` / `ekspresowe (do 48h)`
- Wpływa na wyróżnienie w feedzie

**Lokalizacja realizacji**
- Auto-wypełniana z adresu operacyjnego firmy
- Możliwość zmiany jeśli lokalizacja jest inna (np. inny oddział)

---

## 6. Struktura sygnału — pola branżowe

Model materiałowy (gałęzie 1–8) i model usługowy (gałęzie 9–12).

---

### Model materiałowy — pola wspólne dla gałęzi 1–8

| Pole | Typ | Uwagi |
|------|-----|-------|
| Materiał / polimer | multi-select z katalogu polimerów | Główny filtr feedu |
| Forma materiału | select — specyficzny dla gałęzi | patrz poniżej |
| Ilość | liczba + jednostka (kg / t) | Dla MAMY: ilość dostępna; dla SZUKAMY: ilość potrzebna |
| Ilość: pełna/częściowa | toggle: `Cała ilość` / `Wybrana ilość` | Dla MAMY — czy nadawca sprzedaje wszystko co ma, czy część |
| Termin dostępności | `od zaraz` / data / `do ustalenia` | |
| Pakowanie | multi-select: `big-bag` / `worek 25 kg` / `luzem` / `inne` | Opcjonalne |
| Transport | `odbiór własny` / `dostawa możliwa` / `do ustalenia` | Opcjonalne |

---

### 6.1 Producent wyrobów z tworzyw sztucznych

**MAMY (podaż):**
- Typ podaży: `nadwyżka wyrobów gotowych` / `przemiał PIR (odpad produkcyjny)` / `wolne moce produkcyjne (tolling)` / `półfabrykat`
- Jeśli moce produkcyjne: technologia (wtrysk/wytłaczanie/etc.), dostępne okna czasowe, szacunkowa zdolność (szt./h lub kg/h)
- Jeśli materiał: forma (`wyrób gotowy` / `przemiał` / `aglomerat`), polimer, ilość

**SZUKAMY (popyt):**
- Typ zapotrzebowania: `surowiec do produkcji` / `zlecenie produkcyjne (podwykonawstwo)` / `narzędzie / forma wtryskowa`
- Jeśli surowiec: polimer, forma (granulat/regranulat), ilość, typ (virgin/recyklat/oba), wymagane certyfikaty
- Jeśli podwykonawstwo: technologia, opis produktu (skrócony), wolumen serii, termin

---

### 6.2 Compounder

**MAMY:**
- Typ: `partia kompoundu w magazynie` / `wolne moce do tollingu`
- Jeśli kompound: polimer bazowy (z katalogu), modyfikacje (GF/FR/talc/etc.), forma (granulat/proszek), ilość, dostępne certyfikaty
- Jeśli tolling: typ modyfikacji które oferuje, przepustowość miesięczna (przedziały z profilu), czas realizacji

**SZUKAMY:**
- Typ: `polimer bazowy do produkcji` / `dodatek / komponent specjalny` / `zlecenie tollingu na zewnątrz`
- Polimer, ilość, wymagane właściwości (pole tekstowe lub multi-select z listy modyfikacji)

---

### 6.3 Producent dodatków, masterbatch i koncentratów

**MAMY:**
- Kategoria produktu (z listy profilu: MB barwiący / funkcyjny / stabilizator / etc.)
- Kompatybilne polimery bazowe (z katalogu)
- Forma (granulat/proszek/płyn/pasta)
- Ilość, MOQ
- Certyfikaty: food-contact / NIR-detectable / RoHS / REACH

**SZUKAMY:**
- Typ: `surowiec nośny (carrier resin)` / `specyfikacja niestandardowa do wyceny` / `zlecenie custom batch`
- Dla custom batch: opis funkcji (pole tekstowe), kompatybilny polimer, ilość, termin, wymagane certyfikaty

---

### 6.4 Recykler

Gałąź z największym naturalnym dopasowaniem do Sygnałów.

**MAMY:**
- Produkt: polimer (z katalogu), forma wyjściowa (`regranulat` / `przemiał` / `aglomerat` / `płatki (shredd)` / `proszek (pulwer)` / `olej pirolityczny`)
- Klasa jakości: `przemysłowa` / `food-contact` / `medyczna`
- Ilość dostępna + toggle pełna/częściowa
- Certyfikaty: RecyClass / Cyclos-HTP / ISO 15270
- Własny transport: tak/nie
- Pakowanie: big-bag / worek 25 kg / luzem

**SZUKAMY:**
- Materiał wejściowy: polimer, forma wejściowa (`bele` / `luzem` / `przemiał` / `folia` / `odpady PIR` / `odpady PCR`)
- Ilość potrzebna (jednorazowo / miesięcznie — radio)
- Minimalna jednorazowa dostawa (z przedziałów profilu)
- Wymagania jakościowe (pole tekstowe)
- Własny odbiór: tak/nie

---

### 6.5 Gospodarka odpadami

**MAMY:**
- Frakcja dostępna do przekazania: polimer (z katalogu + `mix / frakcja mieszana`), forma (`bele` / `big-bag` / `luzem` / `worki`)
- Źródło: `B2B (przemysłowe)` / `komunalne (PCR)` / `mieszane`
- Ilość, termin dostępności
- BDO: numer rejestrowy (auto z profilu) — widoczny na sygnale jako znacznik zaufania
- Własny transport/dostawa: tak/nie

**SZUKAMY:**
- Frakcja poszukiwana do zbiórki/skupu: polimer, forma
- Ilość (jednorazowo lub regularnie)
- Zasięg zbiórki (`lokalny` / `regionalny` / `ogólnopolski`)
- Odbiór własny: tak/nie

---

### 6.6 Dostawca surowców pierwotnych

**MAMY:**
- Materiał: polimer, forma (`granulat` / `proszek` / `płyn` / `arkusze`)
- Producent/marka: (z profilu, np. BASF, Sabic, LyondellBasell)
- Dostępność: `od zaraz` / `przesyłka oczekiwana od [data]`
- Ilość, MOQ
- Wyłącznie virgin: tak (znacznik z profilu)
- Dostawa do klienta: tak/nie

**SZUKAMY:**
- Używane rzadziej — możliwy przypadek: duży nabywca szukający stałego dostawcy konkretnej marki/gatunku
- Materiał, producent preferowany, wolumen roczny, wymagany typ kontraktu (`spot` / `kontrakt stały`)

---

### 6.7 Trader

Obie strony są naturalne — trzon działalności tradera.

**MAMY:**
- Typ materiału: `virgin` / `recyklat` / `regranulat` / `off-spec` / `nadwyżka produkcyjna` / `odpady tworzyw`
- Polimer, forma, ilość, origin (kraj/region — opcjonalne)
- Handel spot: tak/nie
- Eksport: tak/nie

**SZUKAMY:**
- Aktywny skup: polimer, forma, ilość, typ (virgin/recyklat/off-spec)
- Pilność: `pilne` / `regularne zapotrzebowanie` / `jednorazowe`
- Import: tak/nie

---

### 6.8 Broker

Szczególny przypadek — broker nie ma własnego stocku.

**MAMY:**
- Typ: `mogę pozyskać` (nie: "mamy w magazynie")
- Specjalizacja materiałowa lub maszynowa (z profilu)
- Zasięg geograficzny (`krajowy` / `UE` / `poza UE`)
- Opis (pole tekstowe): "Pośredniczę w zakupie i sprzedaży regranulatu PA6 — skontaktuj się jeśli szukasz lub masz nadwyżkę"
- Znacznik: `POŚREDNICTWO` — auto-dodawany do wszystkich sygnałów brokerów, widoczny dla odbiorców

**SZUKAMY:**
- Typ: `szukam w imieniu klienta` (klient anonimowy)
- Materiał/produkt, ilość, termin
- Znacznik `POŚREDNICTWO` — auto-dodawany
- Uwaga: broker nie ujawnia tożsamości klienta; odpowiedź trafia do brokera, który dalej komunikuje

> **Zasada projektowa:** Wszyscy odbiorcy sygnału brokera muszą widzieć że rozmawiają z pośrednikiem, nie bezpośrednim kupcem/sprzedawcą. Znacznik POŚREDNICTWO jest obowiązkowy i niedyskrecjonalny.

---

### Model usługowy — pola wspólne dla gałęzi 9–12

| Pole | Typ | Uwagi |
|------|-----|-------|
| Typ usługi / produktu | select — specyficzny dla gałęzi | |
| Dostępność | `natychmiast` / `od daty` / `do uzgodnienia` | |
| Przepustowość / liczba miejsc | tekst lub liczba | Np. "2 okna projektowe w lipcu" |
| Czas realizacji | przedziały (jak w profilu) | Opcjonalne |
| Zasięg realizacji | `zdalnie` / `na miejscu u klienta` / `w siedzibie firmy` / `oba` | |

---

### 6.9 Maszyny i urządzenia

**MAMY:**
- Kategoria maszyny (z listy profilu)
- Marka, model (wolne pole)
- Rok produkcji
- Stan: `nowa` / `używana` / `odnowiona (refurbished)`
- Kluczowy parametr techniczny (wolne pole, np. "siła zwarcia 350t", "średnica ślimaka 60mm")
- Lokalizacja maszyny (województwo/kraj)
- Serwis i gwarancja: tak/nie

**SZUKAMY:**
- Kategoria maszyny
- Marka preferowana (opcjonalne)
- Stan akceptowany: `nowa` / `używana` / `refurbished` / `dowolny`
- Kluczowy parametr (wolne pole)
- Budżet: nie ujawniany — kontakt przez komunikator

> **Ważna zasada:** Sygnał MAMY — maszyna jest dostępny dla WSZYSTKICH kategorii firm, nie tylko gałęzi "Maszyny i urządzenia". Producent który chce sprzedać własną prasę powinien mieć możliwość wystawienia sygnału bez zmiany kategorii firmy.

---

### 6.10 Komponenty i części zamienne

**MAMY:**
- Typ: `forma wtryskowa do sprzedania` / `części zamienne w magazynie` / `wolne moce serwisowe`
- Jeśli forma: polimer dla którego zaprojektowana, liczba gniazd, max wymiar, stan
- Jeśli części: typ maszyny której dotyczą, marki obsługiwane (wolne pole)
- Jeśli serwis: typ usługi, dostępne terminy

**SZUKAMY:**
- Typ: `potrzebuję formy wtryskowej` / `pilnie szukam części zamiennej` / `zlecę serwis / naprawę`
- Dla formy: polimer, gabaryt, liczba gniazd, termin
- Dla części: marka maszyny, nazwa/kod części (wolne pole), pilność
- Dla serwisu: typ maszyny, opis problemu (wolne pole)

---

### 6.11 Technologia i IT

**MAMY:**
- Kategoria rozwiązania (z profilu: MES / ERP / WMS / CAD / IIoT / etc.)
- Model: `SaaS` / `on-premise` / `wdrożenie na zamówienie`
- Dostępność: wolne miejsca wdrożeniowe / demo / bezpłatny pilot
- Dostępne terminy (np. "Q3 2026, 2 miejsca wdrożeniowe")
- Branże docelowe (z profilu)

**SZUKAMY:**
- Kategoria rozwiązania
- Model preferowany
- Opis wymagań (pole tekstowe, max 400 znaków) — np. "Szukamy WMS dla zakładu recyklingu, ~200t/mies., integracja z BDO"
- Harmonogram projektu: `pilne (do 3 mies.)` / `planowane (3–12 mies.)` / `budżet w trakcie zatwierdzania`

---

### 6.12 Laboratorium i B+R

**MAMY:**
- Typ: `pojemność badawcza (jednorazowe zlecenia)` / `umowy seryjne / stałe` / `projekt B+R`
- Typy badań dostępnych (multi-select z profilu)
- Akredytacja PCA: tak/nie (auto z profilu — znacznik na sygnale)
- Szacowany czas realizacji (przedziały z profilu)
- Dostępność: natychmiast / od daty

**SZUKAMY:**
- Typ: `jednorazowe zlecenie` / `stała współpraca` / `projekt badawczy / B+R`
- Typy badań potrzebnych (multi-select)
- Liczba próbek / partii (opcjonalne)
- Wymagana akredytacja PCA: tak/nie/obojętne
- Pilność: `standardowa` / `pilna (do 5 dni roboczych)` / `ekspresowa (do 48h)`

---

## 7. Dystrybucja — mechanizm "kto widzi"

Każdy sygnał ma ustawienie dystrybucji wybierane przez nadawcę przy tworzeniu.

### Poziomy dystrybucji

| Poziom | Kto widzi | Przypadek użycia |
|--------|-----------|-----------------|
| **Wszyscy** | Wszystkie zweryfikowane firmy na polyGo | Sygnał do szerokiego rynku |
| **Obserwujący** | Firmy które obserwują nadawcę | Dla aktywnej bazy followersów |
| **Ulubione** | Firmy z listy Ulubionych nadawcy | Preferowani partnerzy |
| **Segment** | Nazwana lista kontaktów (np. "Klienci HDPE") | Targetowane rozgłaszanie |
| **Wybrane firmy** | Ręcznie wybrane firmy z katalogu polyGo | Jeden do kilku odbiorców |

### Zasady dystrybucji

- Firma niewidoczna (ustawienie "Brak widoczności" w profilu) nadal może tworzyć sygnały i je wysyłać — ale może ustawiać dystrybucję tylko na poziomach węższych niż "Wszyscy" (max: Obserwujący/Ulubione/Segment/Wybrane). Logika: ukryta firma nie powinna pojawiać się w otwartym feedzie.
- Sygnał może mieć tylko jeden aktywny poziom dystrybucji jednocześnie. Nie ma "wyślij do Segmentu A ORAZ Wybranych firm" — to dwa osobne sygnały.
- Zmiana dystrybucji po publikacji jest możliwa (np. z Ulubionych na Wszyscy) — ale nie cofa powiadomień już wysłanych.

### Segmenty — zarządzanie

- Segmenty tworzone i zarządzane przez Owner/Admin firmy w sekcji Kontakty/CRM
- Segment = nazwana lista firm z katalogu polyGo
- Przykłady: "Klienci HDPE", "Dostawcy recyklatu PP", "Partnerzy w UE"
- Limit segmentów na firmę: TBD (sugestia: 20)

---

## 8. Feed — widok agregowany

### Dostęp

Feed dostępny dla wszystkich zalogowanych użytkowników. Osobna sekcja w nawigacji głównej: **"Sygnały"**.

### Zawartość feedu dla danego użytkownika

Użytkownik widzi sygnały z trzech źródeł:
1. Sygnały ustawione na dystrybucję "Wszyscy"
2. Sygnały adresowane do jego firmy (przez Obserwujących, Ulubione, Segment lub Wybrane firmy)
3. Sygnały od firm które obserwuje (jeśli ustawiono dystrybucję min. "Obserwujący")

Sygnały firmy użytkownika **nie pojawiają się** w jego własnym feedzie.

### Sortowanie domyślne

Chronologiczne — najnowsze na górze. Wyróżnienie dla sygnałów z flagą `pilne` lub `ekspresowe`.

### Filtry feedu

| Filtr | Opcje |
|-------|-------|
| Typ sygnału | MAMY / SZUKAMY / oba |
| Kategoria branżowa | multi-select — 12 kategorii polyGo |
| Materiał / polimer | multi-select z katalogu polimerów |
| Lokalizacja | województwo / kraj |
| Pilność | tylko pilne/ekspresowe |
| Tylko obserwowane firmy | toggle |

Filtry persistowane w sesji. Opcja zapisu preferencji filtrów jako domyślne dla użytkownika.

### Karta sygnału w feedzie

Widok skondensowany — pełne szczegóły po kliknięciu.

```
┌─────────────────────────────────────────────────────────┐
│  [MAMY]  ♻️ Recykler          🕐 2 godz. temu   [🔔]   │
│                                                         │
│  Firma ABC Recycling Sp. z o.o.                         │
│  📍 Śląskie                                             │
│                                                         │
│  24t HDPE PCR regranulat — food-contact, od zaraz       │
│                                                         │
│  Forma: regranulat | Pakowanie: big-bag                 │
│  RecyClass ✓  |  Transport: odbiór własny               │
│                                                         │
│  [Odpowiedz →]                          [⭐ Obserwuj]  │
└─────────────────────────────────────────────────────────┘
```

Elementy karty:
- Badge typu (MAMY zielony / SZUKAMY niebieski) + ikona kategorii branżowej
- Nazwa firmy + województwo
- Tytuł sygnału (pogrubiony)
- Kluczowe atrybuty (max 3 tagi)
- Czas publikacji (relatywny: "2 godz. temu", "wczoraj"; po 7 dniach: data)
- CTA: "Odpowiedz" — otwiera komunikator z kontekstem sygnału
- Przycisk obserwowania firmy
- Ikona dzwonka — zarządzanie alertem dla tego typu sygnału

### Widok szczegółowy sygnału

Po kliknięciu karty — pełna strona/modal z:
- Wszystkimi polami sygnału
- Pełnym opisem
- Danymi kontaktowymi firmy (telefon widoczny jeśli profil publiczny)
- CTA: "Wyślij wiadomość" — otwiera komunikator z cytatem sygnału

---

## 9. Cykl życia sygnału

```
ROBOCZA → AKTYWNA → WYGASŁA
              ↓
          ZAMKNIĘTA (ręcznie)
              ↓
          ZARCHIWIZOWANA
```

### Stany sygnału

| Stan | Widoczność | Opis |
|------|-----------|------|
| **Robocza** | Tylko nadawca | Zapisany szkic, niepublikowany |
| **Aktywna** | Odbiorcy wg dystrybucji | Widoczna w feedzie, aktywuje powiadomienia |
| **Wygasła** | Tylko nadawca | Data ważności minęła lub ilość = 0 |
| **Zamknięta** | Tylko nadawca | Ręcznie zamknięta przez nadawcę (sprawa załatwiona) |
| **Zarchiwizowana** | Tylko Owner/Admin | Wygasłe i zamknięte po 90 dniach |

### Mechanizm wygaśnięcia

**Wygaśnięcie datowe:** System automatycznie przełącza sygnał w stan Wygasła o północy w dniu wygaśnięcia.

**Przypomnienie o odnowieniu:** 3 dni przed wygaśnięciem — powiadomienie in-app + opcjonalnie e-mail do nadawcy: "Twój sygnał wygasa 17 czerwca — odnów jeśli temat jest nadal aktualny."

**Odnowienie:** Jednym kliknięciem — przedłuża ważność o domyślny okres (30 dni) lub nową datę. Nowo-odnowiony sygnał NIE pojawia się jako "nowy" w feedzie odbiorców (nie wywołuje ponownych powiadomień) — chyba że nadawca edytuje treść.

**Wygaśnięcie ilościowe (v3+):** Powiązanie z modułem magazynowym — sygnał MAMY wygasa gdy ilość w magazynie spadnie do 0.

### Edycja aktywnego sygnału

- Zmiana treści, ilości, opisu, daty ważności: dozwolona
- Zmiana dystrybucji: dozwolona (rozszerzenie zakresu może wyzwolić powiadomienia do nowych odbiorców)
- Zmiana typu (MAMY → SZUKAMY): niedozwolona — należy zamknąć i stworzyć nowy sygnał
- Po edycji: znacznik "edytowano [czas]" widoczny na karcie sygnału

### Historia sygnałów

Owner/Admin widzi wszystkie sygnały firmy (aktywne, wygasłe, zamknięte, zarchiwizowane) w sekcji "Moje Sygnały" z filtrem statusu i datą.

---

## 10. Powiadomienia push i alerty

### 10.1 Obserwowanie firm

Użytkownik może obserwować dowolną firmę z katalogu.

**Trigger powiadomienia:** Obserwowana firma publikuje nowy aktywny sygnał (jeśli dystrybucja sygnału obejmuje "Obserwujących" lub szerszą).

**Powiadomienie:**
- Browser push: "ABC Recycling opublikowało nowy sygnał: 24t HDPE PCR regranulat"
- Kliknięcie → bezpośrednio na kartę sygnału

### 10.2 Alerty materiałowe (subskrypcje)

Użytkownik definiuje kryteria — system powiadamia gdy pojawi się pasujący sygnał.

**Pola alertu:**

| Pole | Obowiązkowe | Opcje |
|------|-------------|-------|
| Typ sygnału | TAK | MAMY / SZUKAMY |
| Kategoria branżowa | NIE | multi-select |
| Materiał / polimer | NIE | multi-select z katalogu |
| Forma materiału | NIE | multi-select |
| Minimalna ilość | NIE | liczba + jednostka |
| Lokalizacja | NIE | województwo / kraj |

Minimum: typ sygnału + przynajmniej jedno z pozostałych.

**Zarządzanie alertami:**
- Max 10 alertów na użytkownika
- Alert można pauzować bez usuwania
- Podgląd alertów w ustawieniach konta: "Moje alerty"

**Kanały powiadomień:**
- Browser push (opcja włączania przy tworzeniu pierwszego alertu)
- Powiadomienie in-app (centrum powiadomień — dzwonek)
- E-mail (opcja w ustawieniach konta: natychmiast / digest dzienny / wyłączony)

**Digest dzienny:** Zbiorcze powiadomienie e-mail z listą nowych sygnałów pasujących do alertów z ostatnich 24h. Format: lista kart z CTA "Zobacz sygnał". Wysyłany o 8:00 dla użytkowników z alertami e-mail w trybie digest.

### 10.3 Powiadomienie o odpowiedzi na sygnał

Gdy ktoś kliknie "Odpowiedz" na sygnał i wyśle pierwszą wiadomość przez komunikator — nadawca sygnału dostaje powiadomienie: "Firma XYZ odpowiedziała na Twój sygnał: [tytuł]". Kliknięcie otwiera wątek komunikatora.

### 10.4 Centrum powiadomień (dzwonek)

Wszystkie powiadomienia związane z Sygnałami agregowane w centrum powiadomień. Oddzielna zakładka "Sygnały" obok zakładki "Wiadomości".

---

## 11. Powiązania z innymi modułami

### Komunikator

Kluczowa integracja. Przycisk "Odpowiedz" na każdym sygnale otwiera nowy wątek komunikatora z:
- Automatycznym cytatem sygnału w pierwszej wiadomości (nadawca widzi kontekst)
- Tagiem "[Sygnał]" w nagłówku wątku

Jeśli rozmowa z daną firmą już istnieje — pojawia się wybór: "Nowy wątek (dot. sygnału)" lub "Wyślij do istniejącego wątku".

### Profil firmy

- Na profilu firmy (widok publiczny) pojawia się sekcja "Aktywne Sygnały" — lista sygnałów tej firmy ustawionych na dystrybucję "Wszyscy" lub "Obserwujący" (jeśli oglądający obserwuje tę firmę)
- Umożliwia to przeglądanie sygnałów konkretnej firmy bez wchodzenia do głównego feedu

### Ulubione i Segmenty

- Listy Ulubionych i Segmentów tworzone w module Kontakty są bezpośrednio dostępne jako opcja dystrybucji przy tworzeniu sygnału
- Jeśli firma jest dodana do Ulubionych innego użytkownika — może targetować go sygnałem przez poziom "Ulubione"

### Katalog firm

- Katalog firm i feed Sygnałów są odrębnymi widokami, ale powiązanymi
- Z karty firmy w katalogu można przejść do jej aktywnych sygnałów
- Z karty sygnału można przejść na profil firmy-nadawcy

---

## 12. Kluczowe przepływy UX

### Przepływ A: Tworzenie sygnału

```
Nawigacja → "Sygnały" → "Nowy sygnał"
→ Wybór: MAMY / SZUKAMY
→ Wybór kategorii branżowej (jeśli firma ma kilka)
→ Formularz (pola wspólne + pola branżowe)
→ Dystrybucja: kto zobaczy
→ Podgląd karty sygnału
→ "Opublikuj"
→ Potwierdzenie + link do sygnału w feedzie
```

Auto-zapis wersji roboczej co 30 sekund. Użytkownik może wrócić do szkicu.

### Przepływ B: Przeglądanie feedu i odpowiedź

```
Nawigacja → "Sygnały"
→ Feed (domyślne filtry użytkownika)
→ Kliknięcie karty sygnału → widok szczegółowy
→ "Odpowiedz" → komunikator z cytatem sygnału
→ Wpisanie wiadomości → wyślij
```

### Przepływ C: Ustawianie alertu

```
Nawigacja → "Sygnały" → "Moje Alerty" → "Nowy alert"
→ Typ sygnału (MAMY / SZUKAMY)
→ Opcjonalne filtry (materiał, ilość, lokalizacja, branża)
→ Kanał powiadomień (push / e-mail / oba)
→ Zapisz
→ Potwierdzenie z listą aktywnych alertów
```

Alternatywna ścieżka: kliknięcie ikony dzwonka na karcie sygnału w feedzie → "Utwórz alert dla tego typu sygnału" → formularz z pre-wypełnionymi wartościami z tej karty.

### Przepływ D: Zamknięcie sygnału

```
"Moje Sygnały" → wybór aktywnego sygnału → "Zamknij sygnał"
→ Opcjonalny powód (wewnętrzny, niewidoczny dla innych):
  "Sprawa załatwiona" / "Materiał wyprzedany" / "Inne"
→ Potwierdzenie → sygnał przechodzi w stan Zamknięta
```

---

## 13. Decyzje produktowe

| Obszar | Decyzja |
|--------|---------|
| **Ceny** | Ceny nie są polem sygnału — negocjacja przez komunikator. Platforma nie uczestniczy w transakcji. |
| **Broker — anonimowość klienta** | Broker może publikować sygnał SZUKAMY bez ujawniania klienta, ale znacznik POŚREDNICTWO jest obowiązkowy i niedyskrecjonalny. |
| **Maszyny dla wszystkich gałęzi** | Sygnał MAMY — maszyna dostępny dla WSZYSTKICH firm, nie tylko gałęzi "Maszyny". Każda firma może sprzedać własny sprzęt. |
| **Firma ukryta** | Firma z "Brak widoczności" może tworzyć sygnały, ale nie może ustawiać dystrybucji "Wszyscy" — max "Obserwujący" lub wężej. |
| **Sygnał = jedna kategoria** | Jeden sygnał = jedna kategoria branżowa. Firma wielobranżowa tworzy osobne sygnały dla każdej kategorii. |
| **Historia dla Owner/Admin** | Pełna historia sygnałów firmy (włącznie z wygasłymi i zamkniętymi) widoczna dla Owner/Admin. Pracownicy widzą tylko swoje sygnały + aktywne firmy. |
| **Odnowienie** | Odnowiony sygnał nie wyzwala ponownych powiadomień chyba że zmieniono treść. |
| **Dystrybucja — jeden poziom** | Sygnał ma jeden aktywny poziom dystrybucji. Chęć dotarcia do kilku różnych grup = kilka sygnałów. |
| **Moderacja admina** | Admin polyGo może ukryć lub usunąć sygnał naruszający zasady. Nadawca dostaje powiadomienie z powodem. |
| **Widoczność sygnałów dla admina** | Admin polyGo widzi WSZYSTKIE sygnały niezależnie od poziomu dystrybucji (włącznie z "Wybrane firmy") — niezbędne dla moderacji. |
| **Limit sygnałów** | Start: max 10 aktywnych sygnałów na firmę. Cel: ochrona feedu przed zdominowaniem przez jedną firmę gdy sieć jest mała. Cap do zniesienia gdy sieć osiągnie dojrzałość (~200+ aktywnych firm). |
| **Firma zablokowana** | Blokada firmy przez admina → wszystkie aktywne sygnały znikają z ekosystemu natychmiast. Zgodnie z zasadą: niezweryfikowana/zablokowana firma jest niewidoczna wszędzie, zawsze. |

---

## 14. Poza zakresem v2

Poniższe elementy są świadomie wykluczone z v2 i mogą być rozważone w v3+:

| Funkcja | Powód odroczenia |
|---------|-----------------|
| Integracja z modułem magazynowym (auto-wygaśnięcie ilościowe) | Moduł magazynowy sam w sobie jest poza MVP/v2 |
| Cennik / widełki cenowe na sygnale | Wrażliwe handlowo; negocjacja w komunikatorze wystarczy |
| Publiczny feed (bez logowania) | Sprzeczne z filozofią zamkniętej sieci |
| Grupowy chat sygnałowy (wiele firm reaguje publicznie) | Złożoność moderacji; v3+ |
| Wyszukiwarka semantyczna / AI w feedzie | v3+ |
| API eksportu sygnałów do ERP | v3+ |
| Digest tygodniowy | v3 — digest dzienny wystarczy na start |
| Alerty SMS | v3 — push + e-mail wystarczy na start |
| Statystyki sygnału dla Owner (ile wyświetleń, ile odpowiedzi) | Wartościowe — rozważyć w v2.1 |
| Klonowanie sygnału | QoL feature — rozważyć w v2.1 |
| Oceny / feedback po transakcji | Poza zakresem platformy — polyGo nie uczestniczy w transakcji |

---

## 15. Otwarte pytania

| # | Pytanie | Kontekst |
|---|---------|----------|
| 1 | **Czy szkice mają termin ważności?** | Szkice nigdy nie wygasają vs. auto-usuwanie po 30 dniach bez publikacji |
| 2 | **Sygnały wielojęzyczne?** | Na start platforma PL. Czy firmy z UE mogą pisać sygnały po angielsku? |
| 3 | **Statystyki sygnałów dla Owner?** | "Twój sygnał był widziany X razy, Y firm odpowiedziało" — wartościowe, ale złożone. v2 czy v2.1? |
| 4 | **Klonowanie sygnału?** | Szybkie tworzenie nowego sygnału na podstawie poprzedniego — niska złożoność, duże QoL. v2 czy v2.1? |

### Zamknięte

| # | Pytanie | Decyzja |
|---|---------|---------|
| ✓ | Limit aktywnych sygnałów na firmę? | Start: 10. Cap do zniesienia przy ~200+ firmach. |
| ✓ | Widoczność sygnałów dla admina polyGo? | TAK — admin widzi wszystko niezależnie od dystrybucji. |
| ✓ | Co się dzieje z sygnałami gdy firma zostaje zablokowana? | Znikają z ekosystemu natychmiast. |

---

*Dokument: sygnaly-feature-spec-v1 | Data: czerwiec 2026 | Wersja: 1*
*Następny krok: przegląd z cofounderem → szacowanie złożoności → wpis do roadmapy v2*
