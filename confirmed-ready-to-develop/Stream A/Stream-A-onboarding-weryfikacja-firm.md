# 🔄 Stream A — Onboarding & weryfikacja firm w polyGo

> **Charakter dokumentu:** dokumentacja biznesowa Streamu A. Opisuje **co się dzieje** na ścieżce od zaproszenia firmy do operacyjnego zespołu pracowników w polyGo, bez wchodzenia w szczegóły techniczne (model danych, API, infrastruktura).

---

## Co to jest

Stream A to **pierwszy i bazowy potok** platformy polyGo — zamkniętej, manualnie weryfikowanej platformy B2B dla polskiej branży tworzyw sztucznych i powiązanych branż. Żadna firma nie wchodzi do systemu bez przejścia tego potoku. Zamknięta natura platformy to świadomy "moat" — przewaga, nie ograniczenie.

Stream A pokrywa pełną drogę od **wysłania zaproszenia przez Admina platformy** do **w pełni operacyjnej firmy z zespołem pracowników**.

> **Dwie ścieżki onboardingu (ten sam efekt końcowy):**
> 1. **Self-service przez Ownera** — Admin wysyła zaproszenie, Owner sam zakłada firmę (ścieżka domyślna, opisana w krokach 1–5 poniżej).
> 2. **Manual przez Admina** — Admin platformy zakłada firmę **za** Ownera (np. po targach, telefonicznie, gdy Owner nie chce/nie umie sam wypełnić formularza). Admin używa tych samych formularzy co Owner, wpisuje dane firmy + dane kontaktowe Ownera; po zapisie Owner dostaje e-mail z linkiem aktywacyjnym i wchodzi na gotowy, już aktywny profil. Patrz **Krok 2-alt** poniżej.

---

## Flow krok po kroku

### **Krok 1 — Admin platformy zaprasza firmę** *(ścieżka self-service)*
Admin platformy (Maciek) ręcznie wysyła e-mail z **unikatowym linkiem zapraszającym** do konkretnej firmy. Bez tego linku nie ma możliwości rejestracji — platforma jest **invitation-only**, brak publicznego formularza.

---

### **Krok 2 — Owner zakłada konto i rejestruje firmę**
Właściciel/przedstawiciel firmy klika link → trafia na stronę zaproszenia → naciska **"Create Company"** → wypełnia dwa formularze:

**2a. Dane firmy (Identyfikacja prawna):**
- Nazwa prawna firmy *(obowiązkowe)*
- NIP — format `10 cyfr` lub `PL + 10 cyfr` *(obowiązkowe; podstawa weryfikacji w GUS)*
- KRS — `10 cyfr` *(opcjonalne — JDG nie ma KRS)*
- Adres siedziby (ulica/nr budynku/nr lokalu/kod/miasto/kraj) *(obowiązkowe)*
- Strona WWW *(opcjonalne)*

**2b. Dane osobiste Ownera (Company Owner):**
- Imię i nazwisko *(obowiązkowe)*
- E-mail *(obowiązkowe)*
- Telefon *(obowiązkowe)*

System sprawdza czy e-mail już jest zarejestrowany. Jeśli nie — tworzy konto i przypisuje rolę **Administrator (Company Owner)**. Pierwszy user firmy automatycznie dostaje uprawnienia Admina.

System wysyła na e-mail Ownera **verification link** (osobny od zaproszenia). Owner widzi ekran *"Twoja firma czeka na weryfikację"*. Firma trafia do kolejki oczekujących na weryfikację Admina.

---

### **Krok 2-alt — Admin platformy zakłada firmę za Ownera** *(ścieżka manual)*
Admin loguje się do swojego panelu i naciska **"Create company on behalf of owner"**. Wypełnia **te same dwa formularze** co Owner w Kroku 2 (dane firmy + dane kontaktowe Ownera) — Admin jest tu operatorem, nie nowym właścicielem. Email Ownera w formularzu = przyszły login Ownera.

Po zapisie:
- Firma jest od razu **aktywna** (Admin sam ją zakłada, więc weryfikacja Kroku 3 jest już wykonana implicite — Admin odpowiada za poprawność danych)
- System wysyła Ownerowi e-mail *"Założyliśmy Ci profil firmy w polyGo — ustaw hasło i wejdź"*
- Owner klika link, ustawia hasło, loguje się → wchodzi od razu na **Krok 4** (uzupełnianie profilu) na już aktywnej firmie

> **Dlaczego ta ścieżka istnieje:** po targach / rozmowach telefonicznych Owner często nie chce / nie ma czasu wypełniać formularza. Admin może go "wnieść" do platformy ręcznie i Owner dostaje gotowe konto. Niezbędne dla strategii ręcznego zasiedlania w fazie pierwszych firm.

> **Uwaga:** w ścieżce manualnej Admin **nie staje się** właścicielem firmy. Wpisany email Ownera = ten użytkownik dostaje rolę Company Owner. Admin platformy nadal jest osobnym kontem z osobnymi uprawnieniami. Jedyna firma, której Admin platformy jest właścicielem, to jego własna (jeśli ją zakłada).

> **Audyt:** firmy założone tą ścieżką muszą być rozpoznawalne (kto je założył i kiedy) — na potrzeby supportu i ewentualnej re-weryfikacji.

---

### **Krok 3 — Admin platformy weryfikuje i podejmuje decyzję**
W panelu Admina platformy pojawia się firma w kolejce oczekujących. Admin:
1. Przegląda NIP (weryfikuje w GUS), KRS (jeśli podany), dane kontaktowe, adres
2. Podejmuje decyzję: **Aktywuj** albo **Odrzuć z uzasadnieniem**

**Przy aktywacji:** firma staje się aktywna, Owner dostaje e-mail *"Twoja firma została zweryfikowana — możesz zaczynać"*.
**Przy odrzuceniu:** firma odrzucona, Owner dostaje e-mail z powodem.

> **Uwaga:** edycja NIP lub KRS po aktywacji cofa firmę do ponownej weryfikacji przez Admina.

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
Lista alfabetyczna od ABS do XPS, z modyfikatorami (GF, FR, High Heat, Impact Modified itd.). Katalog zarządzany przez Admina platformy — Owner może zaproponować brakujący polimer, Admin zatwierdza, wtedy pozycja staje się globalnie dostępna.

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

---

#### 🔑 Charakterystyka firmy — dlaczego Krok 4 to serce platformy

Sektor, do którego polyGo wchodzi, to **kilka połączonych ze sobą branż**, każda z osobną charakterystyką. Profil firmy jest narzędziem, dzięki któremu **inni znajdą tę firmę** przy wyszukiwaniu kontrahenta — jeśli firma się źle scharakteryzuje, jest niewidoczna mimo że jest aktywna. Z perspektywy biznesowej Krok 4 jest fundamentem całego value proposition platformy.

Zasady, które kształtują ten krok:

**a) Firma działa w kilku branżach naraz.**
Realnie wiele firm operuje w więcej niż jednej kategorii (np. Producent + Recykler, albo Trader + Broker). Multi-select kategorii to twarde wymaganie biznesowe — wybór dwóch kategorii pokazuje firmie sumę pól obu sekcji.

**b) Lista kategorii i pól będzie rosła.**
Dziś 12 kategorii, ale rynek się rozwija — Admin platformy musi mieć możliwość dodania nowej kategorii i nowych pól bez czekania na wydanie nowej wersji aplikacji. Każda kategoria niesie własny zestaw pytań (technologie przetwórstwa, park maszynowy, BDO, frakcje wejściowe/wyjściowe, certyfikaty, segmenty rynku itd.) i Admin powinien móc nimi zarządzać sam.

**c) Profil i wyszukiwarka są jednym źródłem prawdy.**
Każde pole z oznaczeniem `Wyszukiwalne: TAK` w spec v3 musi pojawiać się jako **filtr w katalogu firm**. Innymi słowy: jeśli Admin doda nowe wyszukiwalne pole, w wyszukiwarce katalogu firm pojawia się dla niego filtr — bez osobnego zlecenia. Wyszukiwarka jest pochodną profilu, nie produktem rozwijanym osobno.

**d) Polimery to wspólny katalog dla całej platformy.**
103 polimery to stan startowy, nie zamknięta lista. Owner wybiera z gotowej listy; jeśli brakuje pozycji — proponuje, Admin zatwierdza, wtedy polimer staje się globalnie dostępny dla wszystkich firm. Polimery **nie** są wpisywane jako wolny tekst (to zniszczyłoby wyszukiwarkę).

**e) Certyfikaty — analogicznie do polimerów.**
Lista certyfikatów (ISO 9001, 14001, IATF, RecyClass itd.) to zarządzany centralnie katalog. Filtr "pokaż firmy z certyfikatem X" działa od razu po dodaniu certyfikatu do katalogu.

**f) Doświadczenie wypełniania profilu musi być stopniowane.**
Owner nie widzi 200 pól naraz. Wybór kategorii → rozwija się sekcja tej kategorii. Bez tego firmy zostawią profile niedokończone, a niedokończony profil = niewidoczna firma.

**g) Profil można edytować w dowolnym momencie.**
Po aktywacji Owner może wracać do profilu, dodawać kategorie, zmieniać pola, zmieniać widoczność. Edycja profilu **nie** wymaga ponownej weryfikacji firmy — ponowną weryfikację triggeruje tylko edycja NIP lub KRS.

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

> **Ważne:** rejestracja pracownika jest **admin-driven, nie self-service**. Pracownicy **nie** rejestrują się samodzielnie z osobnego linka — to Owner ich dodaje ręcznie. Tylko Owner (Admin firmy) może dodawać/edytować/usuwać pracowników.

---

## Stan końcowy Streamu A

Po zakończeniu Streamu A firma jest **w pełni operacyjna**:
- ✅ Zweryfikowana i aktywna
- ✅ Z pełnym profilem branżowym (kategorie + materiały + certyfikaty)
- ✅ Z zespołem pracowników
- ✅ Z ustawioną widocznością (Pełna / Brak)
- ✅ Wyszukiwalna w katalogu firm po wszystkich polach oznaczonych jako wyszukiwalne

Firma może szukać kontrahentów i pisać na chacie → to już kolejne streamy (B, C, D, E).