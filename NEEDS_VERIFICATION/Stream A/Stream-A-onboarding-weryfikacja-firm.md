# 🔄 Stream A — Onboarding & weryfikacja firm w polyGo (wersja spójna)

> **Źródła:** POL-42 (Linear) + UF-01/UF-02/UF-03 (repo `User flows/`) + `Company profile/polygo_formularz_rejestracji_v3.md`
> **Status:** propozycja do wklejenia w POL-42

---

## Co to jest

Stream A to **pierwszy i bazowy potok** platformy polyGo — zamkniętej, manualnie weryfikowanej platformy B2B dla polskiej branży tworzyw sztucznych i powiązanych branż. Żadna firma nie wchodzi do systemu bez przejścia tego potoku. Zamknięta natura platformy to świadomy "moat" — przewaga, nie ograniczenie.

Stream A pokrywa pełną drogę od **wysłania zaproszenia przez Admina platformy** do **w pełni operacyjnej firmy z zespołem pracowników**.

---

## Flow krok po kroku

### **Krok 1 — Admin platformy zaprasza firmę**
Admin platformy (Maciek) ręcznie wysyła e-mail z **unikatowym linkiem zapraszającym** (invitation URL z invitation code) do konkretnej firmy. Bez tego linku nie ma możliwości rejestracji — platforma jest **invitation-only** (FR-001), brak publicznego formularza.

→ *Pokrycie: UF-01 precondition*

---

### **Krok 2 — Owner zakłada konto i rejestruje firmę**
Właściciel/przedstawiciel firmy klika link → trafia na Invitation Page z prefilled invitation code → naciska **"Create Company"** → wypełnia dwa formularze:

**2a. Dane firmy (Identyfikacja prawna):**
- Nazwa prawna firmy *(obowiązkowe)*
- NIP — format `10 cyfr` lub `PL + 10 cyfr` *(obowiązkowe; load-bearing dla weryfikacji)*
- KRS — `10 cyfr` *(opcjonalne — JDG nie ma KRS)*
- Adres siedziby (ulica/nr budynku/nr lokalu/kod/miasto/kraj) *(obowiązkowe)*
- Strona WWW *(opcjonalne)*

**2b. Dane osobiste Ownera (Company Owner):**
- Imię i nazwisko *(obowiązkowe)*
- E-mail *(obowiązkowe)*
- Telefon *(obowiązkowe)*

System sprawdza czy e-mail już jest zarejestrowany. Jeśli nie — tworzy konto i przypisuje rolę **Administrator (Company Owner)**. Pierwszy user firmy automatycznie dostaje uprawnienia Admina.

System wysyła na e-mail Ownera **verification link** (osobny od invitation linka). Owner widzi ekran *"Twoja firma czeka na weryfikację"*. Firma trafia w stan `pending`.

→ *Pokrycie: UF-01 + spec v3 sekcja 2 (Identyfikacja prawna + Dane kontaktowe konta)*

---

### **Krok 3 — Admin platformy weryfikuje i podejmuje decyzję**
W panelu Admina platformy pojawia się firma w kolejce `pending`. Admin:
1. Przegląda NIP (weryfikuje w GUS), KRS (jeśli podany), dane kontaktowe, adres
2. Podejmuje decyzję: **Aktywuj** albo **Odrzuć z uzasadnieniem**

**Przy aktywacji:** status firmy zmienia się na `active`, Owner dostaje e-mail *"Twoja firma została zweryfikowana — możesz zaczynać"*.
**Przy odrzuceniu:** status `rejected`, Owner dostaje e-mail z powodem.

> **Uwaga:** edycja NIP lub KRS po aktywacji resetuje firmę do `pending` i triggeruje re-weryfikację (FR-006).

→ *Brakuje jako osobny UF w repo — do dopisania jako UF-08*

---

### **Krok 4 — Owner uzupełnia profil firmy**
Owner loguje się i wchodzi w **"My Company" → zakładka "Company profile"**. Uzupełnia profil w pięciu sekcjach (pełna spec: `Company profile/polygo_formularz_rejestracji_v3.md`):

**4a. Lokalizacja i zasięg:**
- Województwo głównej działalności *(obowiązkowe, wyszukiwalne)*
- Zasięg działalności: lokalny / ogólnopolski / eksport UE / eksport poza UE *(obowiązkowe, wyszukiwalne)*
- Opcjonalnie: dodatkowe adresy operacyjne (wiele oddziałów)

**4b. Kategorie branżowe — multi-select z 12 kategorii** *(obowiązkowe, wyszukiwalne)*:
🏭 Producent · 🧬 Compounder · 🧪 Producent dodatków/MB · ♻️ Recykler · 🗑️ Gospodarka odpadami · 🔵 Dostawca surowców pierwotnych · 🔄 Trader · 🤝 Broker · ⚙️ Maszyny i urządzenia · 🔧 Komponenty i części zamienne · 💻 Technologia i IT · 🔬 Laboratorium i B+R

Firma może wybrać kilka — wybór **dynamicznie odsłania pola specyficzne** dla każdej kategorii (np. Producent → technologie przetwórstwa, park maszynowy, segmenty rynku; Recykler → typ recyklingu, BDO, frakcje wejściowe/wyjściowe; itd.). Pełna lista pól per kategoria — patrz spec v3 sekcje 4–15.

**4c. Materiały — wybór z katalogu 103 polimerów** *(obowiązkowe dla większości kategorii, wyszukiwalne)*:
Lista alfabetyczna od ABS do XPS, z modyfikatorami (GF, FR, High Heat, Impact Modified itd.). Katalog zarządzany przez Admina platformy — Owner może zaproponować brakujący polimer, Admin zatwierdza, wtedy pozycja staje się globalnie dostępna (FR-007a).

**4d. Profil publiczny i certyfikaty:**
- Logo (PNG/JPG, max 2 MB)
- Galeria zdjęć (do 5, max 5 MB każde)
- Opis firmy (max 600 znaków)
- Rok założenia
- Dokumenty PDF (do 5, max 10 MB każdy — certyfikaty, karty charakterystyk)
- Certyfikaty (ISO 9001, ISO 14001, IATF 16949, ISO 13485, BRC, IFS, RecyClass, inne) — *wyszukiwalne, filtr*

**4e. Widoczność profilu** *(obowiązkowe, można zmienić w dowolnym momencie)*:
- **Pełna widoczność:** wszyscy zalogowani widzą pełne dane + mogą pisać przez komunikator do dowolnego pracownika
- **Brak widoczności:** widoczne tylko nazwa, logo, opis, zdjęcia — komunikator zablokowany; inni mogą wysłać **Zaproszenie** z opcjonalnym **Kodem polecającym**

Owner naciska **"Save profile"** → kompletny profil firmy zapisany.

→ *Pokrycie: UF-02 + spec v3 sekcje 2–16*

---

### **Krok 5 — Owner dodaje pracowników**
Owner wchodzi w **"My Company" → zakładka "Employees"** → naciska **"Add Employee"**. Dla każdego pracownika ustawia:

**5a. Dane personalne** *(wszystkie obowiązkowe)*:
Username, hasło, Imię, Nazwisko, Telefon, E-mail, Stanowisko (Job Title), Dział, Lokalizacja

**5b. Ustawienia konta:**
- Rola (jedna lub więcej)
- Widoczność pracownika dla innych użytkowników
- Zdjęcie profilowe *(opcjonalne)*

Po zapisie pracownik dostaje **e-mail z danymi logowania**. Od tego momentu może się zalogować i działać w polyGo.

> **Ważne:** rejestracja pracownika jest **admin-driven, nie self-service** (FR-008). Pracownicy **nie** rejestrują się samodzielnie z osobnego linka — to Owner ich dodaje ręcznie. Tylko Owner (Admin firmy) może dodawać/edytować/usuwać pracowników.

→ *Pokrycie: UF-03*

---

## Stan końcowy Streamu A

Po zakończeniu Streamu A firma jest **w pełni operacyjna**:
- ✅ Zweryfikowana i aktywna (status `active`)
- ✅ Z pełnym profilem branżowym (kategorie + materiały + certyfikaty)
- ✅ Z zespołem pracowników
- ✅ Z ustawioną widocznością (Pełna / Brak)
- ✅ Indeksowana w wyszukiwarce katalogu firm (po polach `Wyszukiwalne: TAK`)

Firma może szukać kontrahentów i pisać na chacie → to już kolejne streamy (B, C, D, E).

---

## Powiązania z innymi issues w Linear

**POL-42 blokuje:**
- POL-5 — App shell, router i AuthContext baseline

**Powiązany z:**
- POL-7 — Owner signup flow *(uwaga: do uzgodnienia — POL-7 zakłada 2 ścieżki, ale w spec v3 jest tylko 1 — invitation-only)*

**Do utworzenia:**
- **POL-NEW1** — UF-08: Platform Admin verifies & activates company (Krok 3)
- **POL-NEW2** — Formularz rejestracji firmy: 12 kategorii branżowych + katalog polimerów + filtry wyszukiwania (Krok 4, implementacja spec v3)

---

## Source of truth dla developera

| Dokument | Zawartość |
|---|---|
| `User flows/UF-01-company-registration-via-invitation.md` | Krok 1–2 (registration flow) |
| `User flows/UF-02-company-profile-setup.md` | Krok 4 (profile setup flow) |
| `User flows/UF-03-adding-employees.md` | Krok 5 (adding employees flow) |
| `Company profile/polygo_formularz_rejestracji_v3.md` | **Pełna spec pól formularza** (krok 2 + 4) — 12 kategorii, 103 polimery, decyzje produktowe |
| `Company profile/README_formularz.md` | Jak czytać spec v3 + implikacje dla modelu danych |
| `prd.md` | FR-001 (invitation-only), FR-006 (re-weryfikacja po edycji NIP/KRS), FR-007a (proponowanie polimerów), FR-008 (admin-driven employees) |
| **brak** | Krok 3 — UF-08 do napisania |

---

## Co się zmieniło względem oryginalnego POL-42

| Element | Stary POL-42 | Nowa wersja |
|---|---|---|
| Krok 1 (invitation) | ✅ OK | bez zmian |
| Krok 2 — dane firmy | "nazwa, NIP, KRS, adres, www" | doprecyzowane: NIP obowiązkowy, KRS **opcjonalny**, format NIP, multi-adresy, dane Ownera osobno |
| Krok 2 — verification email | brak | **dodane** (osobno od invitation linka) |
| Krok 3 — weryfikacja Admina | "Admin przegląda i decyduje" *(jednozdaniowo)* | **rozpisany flow** + statusy `pending`/`active`/`rejected` + maile, do zrobienia UF-08 |
| Krok 4 — profil | "opis + materiały PE/PP/PVC" | **12 kategorii multi-select + dynamiczne pola + 103 polimery + widoczność + załączniki + certyfikaty** |
| Krok 5 — pracownicy | "każdy pracownik klika swój link, rejestruje się" | **admin-driven**: Owner ręcznie dodaje, pracownik dostaje e-mail z loginem |
| Materiały | konkretne PE/PP/PVC | katalog 103 polimerów (spec v3 sekcja 16) |
| Widoczność | brak | **dodana** jako pełnoprawny element profilu |
| Załączniki | brak | **dodane** (logo, zdjęcia, PDF) |
