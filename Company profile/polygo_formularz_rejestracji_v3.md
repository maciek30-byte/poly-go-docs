# polyGo — Formularz rejestracji firm
> **Wersja:** 3 | **Data:** czerwiec 2026  
> **Przeznaczenie:** specyfikacja pól formularza rejestracji firmy w platformie polyGo — wejście dla developera.  
> **Zakres:** pola wspólne dla wszystkich firm + pola specyficzne dla 12 kategorii branżowych + katalog polimerów.

---
## Spis treści
1. [Założenia ogólne](#1-założenia-ogólne)
2. [Pola wspólne dla wszystkich firm](#2-pola-wspólne-dla-wszystkich-firm)
3. [Kategorie branżowe — przegląd](#3-kategorie-branżowe--przegląd)
4. [Producent wyrobów z tworzyw sztucznych](#4-producent-wyrobów-z-tworzyw-sztucznych)
5. [Compounder](#5-compounder)
6. [Producent dodatków, masterbatch i koncentratów](#6-producent-dodatków-masterbatch-i-koncentratów)
7. [Recykler](#7-recykler)
8. [Gospodarka odpadami](#8-gospodarka-odpadami)
9. [Dostawca surowców pierwotnych](#9-dostawca-surowców-pierwotnych)
10. [Trader](#10-trader)
11. [Broker](#11-broker)
12. [Maszyny i urządzenia](#12-maszyny-i-urządzenia)
13. [Komponenty i części zamienne](#13-komponenty-i-części-zamienne)
14. [Technologia i IT](#14-technologia-i-it)
15. [Laboratorium i B+R](#15-laboratorium-i-br)
16. [Katalog polimerów](#16-katalog-polimerów)
17. [Decyzje produktowe — podsumowanie](#17-decyzje-produktowe--podsumowanie)

---
## 1. Założenia ogólne
- **Rejestracja wyłącznie przez zaproszenie** — brak publicznego formularza rejestracyjnego.
- **Kategoria branżowa to multi-select** — firma może należeć do kilku kategorii jednocześnie. Wybór kategorii dynamicznie odsłania pola specyficzne dla tej branży.
- **Widoczność profilu** — firma wybiera poziom widoczności przy rejestracji, może go zmienić w dowolnym momencie.
- **Katalog polimerów** — zamknięta lista zarządzana przez admina polyGo. Firma wybiera materiały z listy. Brakujące mogą być proponowane przez właściciela firmy i zatwierdzone przez admina.
- **Wyszukiwalne** — pola oznaczone jako `Wyszukiwalne: TAK` są indeksowane i dostępne jako filtry w katalogu firm.

---
## 2. Pola wspólne dla wszystkich firm
Pola wypełniane przez każdą firmę niezależnie od kategorii branżowej.

### Identyfikacja prawna

**Nazwa prawna firmy**  
- Typ: `tekst jednoliniowy`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Pobierana z GUS lub wpisywana ręcznie przy rejestracji*  

**NIP**  
- Typ: `tekst — walidacja: 10 cyfr lub format PL+10 cyfr (PL1112223344)`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Format PL-prefix obsługuje firmy zagraniczne zarejestrowane w Polsce. Load-bearing dla weryfikacji admina.*  

**KRS**  
- Typ: `tekst — 10 cyfr, opcjonalne`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Opcjonalne — jednoosobowa działalność gospodarcza nie posiada KRS*  

**Adres siedziby**  
- Typ: `ulica / nr budynku / nr lokalu (opcjonalny) / kod pocztowy / miasto / kraj`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Do weryfikacji prawnej, niepubliczny w MVP. Osobne pola na nr budynku i lokalu.*  

**Strona WWW**  
- Typ: `URL`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Wyświetlana na profilu publicznym*  

**Adres prowadzenia działalności (inny niż siedziby)**  
- Typ: `checkbox TAK/NIE → jeśli TAK: nazwa oddziału (opcjonalna) / ulica / nr budynku / nr lokalu / kod pocztowy / miasto. Możliwość dodania wielu lokalizacji.`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Wiele firm ma siedzibę pod innym adresem niż zakład. Obsługa wielu oddziałów.*  

### Lokalizacja i zasięg

**Województwo (główna działalność operacyjna)**  
- Typ: `dropdown — 16 województw`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Główny filtr lokalizacyjny v1*  

**Zasięg działalności**  
- Typ: `multi-select: `lokalny` / `ogólnopolski` / `eksport UE` / `eksport poza UE``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Obowiązkowe — potwierdzone jako istotny filtr dla kupców*  

### Typ działalności

**Kategoria branżowa**  
- Typ: `multi-select — 12 kategorii polyGo (patrz sekcja 3)`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Wybór kategorii dynamicznie odsłania pola specyficzne poniżej. Multi-select — firmy działają w kilku branżach.*  

### Profil publiczny

**Logo firmy**  
- Typ: `upload PNG/JPG — max 2 MB`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Wyświetlane w wynikach wyszukiwania i na profilu*  

**Zdjęcia (galeria)**  
- Typ: `upload — do 5 zdjęć, max 5 MB każde`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Hala produkcyjna, maszyny, magazyn*  

**Opis firmy**  
- Typ: `tekst wieloliniowy — max 600 znaków`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Swobodny opis, niefiltrowany*  

**Rok założenia**  
- Typ: `liczba — rok (np. 1998)`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Widoczny publicznie na profilu*  

**Dokumenty firmowe (PDF)**  
- Typ: `upload PDF — do 5 plików, max 10 MB każdy`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Certyfikaty, badania, karty charakterystyk*  

### Certyfikaty

**Certyfikaty jakości / środowiskowe**  
- Typ: `multi-select: `ISO 9001` / `ISO 14001` / `IATF 16949` / `ISO 13485` / `BRC` / `IFS` / `RecyClass` / `inne` + wolne pole`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Filtr wyszukiwania. RecyClass dodany. Uwaga: niektóre firmy wymagają konkretnego certyfikatu od partnera handlowego.*  

### Dane kontaktowe konta (Company Owner)

**Imię i nazwisko właściciela konta**  
- Typ: `tekst`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Widoczne tylko dla admina polyGo*  

**E-mail właściciela konta**  
- Typ: `e-mail`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Widoczne tylko dla admina polyGo*  

**Telefon właściciela konta**  
- Typ: `telefon`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Widoczne tylko dla admina polyGo*  

### Widoczność profilu

**Poziom widoczności**  
- Typ: `radio: `Pełna widoczność` / `Brak widoczności``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Opcja zmiany w dowolnym momencie.*  

> **Pełna widoczność:** wszyscy użytkownicy widzą pełne dane firmy i mogą pisać przez komunikator z dowolnym pracownikiem.  
> **Brak widoczności:** widoczne tylko nazwa firmy, logo, opis, zdjęcia — komunikator zablokowany. Pozostali użytkownicy mogą wysłać **Zaproszenie** z opcjonalnym **Kodem polecającym**.

---
## 3. Kategorie branżowe — przegląd
Firma wybiera jedną lub więcej kategorii (multi-select). Każda kategoria odsłania dodatkowy zestaw pól specyficznych.

| # | Kategoria | Odpowiednik w Types of Activity |
|---|-----------|--------------------------------|
| 1 | 🏭 Producent | Producer |
| 2 | 🧬 Compounder | *(własna kategoria)* |
| 3 | 🧪 Producent dodatków | *(własna kategoria)* |
| 4 | ♻️ Recykler | Recycler |
| 5 | 🗑️ Gospodarka odpadami | Waste management |
| 6 | 🔵 Dostawca surowców pierwotnych | Virgin materials supplier |
| 7 | 🔄 Trader | Trader |
| 8 | 🤝 Broker | *(własna kategoria)* |
| 9 | ⚙️ Maszyny i urządzenia | Machinery and equipment supplier |
| 10 | 🔧 Komponenty i części zamienne | Components and spare parts supplier |
| 11 | 💻 Technologia i IT | Technology / IT supplier |
| 12 | 🔬 Laboratorium i B+R | *(własna kategoria)* |

---
## 4. Producent wyrobów z tworzyw sztucznych
Obejmuje wszystkie technologie przetwórstwa: wtrysk, wytłaczanie, blow moulding, termoformowanie i inne.

### Technologie przetwórstwa

**Stosowane technologie**  
- Typ: `multi-select: `wtrysk (injection moulding)` / `wytłaczanie (extrusion)` / `wytłaczanie z rozdmuchiwaniem (blow moulding)` / `termoformowanie` / `rotomoulding` / `prasowanie` / `laminowanie` / `druk 3D` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Kluczowy filtr. Multi-select — firmy często łączą technologie.*  

**Własna narzędziownia / toolroom**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Firma z własną narzędziownią = inny profil oferty i możliwości*  

### Materiały

**Materiały przetwarzane**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Surowce (virgin / recyklat)**  
- Typ: `multi-select: `wyłącznie virgin` / `wyłącznie recyklat` / `obydwa``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Ważny filtr — PPWR wymusza rosnący udział recyklatu w produktach*  

### Park maszynowy — wtrysk

**Siła zwarcia (zakres parku)**  
- Typ: `przedziały: `do 100 t` / `100–500 t` / `500–1500 t` / `powyżej 1500 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Wypełnić jeśli wybrano technologię wtrysk*  

**Liczba maszyn wtryskowych**  
- Typ: `przedziały: `1–5` / `6–15` / `16–30` / `powyżej 30``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Park maszynowy — wytłaczanie

**Typ linii wytłaczarskich**  
- Typ: `multi-select: `linia folii` / `linia rur i profili` / `linia arkuszy i płyt` / `linia powlekania` / `linia współwytłaczania (coextrusion)` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Wypełnić jeśli wybrano technologię wytłaczanie*  

### Segmenty i zastosowania

**Segmenty rynku obsługiwane**  
- Typ: `multi-select: `opakowania elastyczne` / `opakowania sztywne` / `automotive` / `AGD i elektronika użytkowa` / `elektronika i elektrotechnika` / `medycyna i farmacja` / `budownictwo` / `rolnictwo` / `przemysł ogólny` / `meble i wyposażenie` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Firmy z doświadczeniem w danym segmencie mają odpowiednie procesy i certyfikaty — ważny filtr*  

**Typowa seria produkcyjna**  
- Typ: `multi-select: `jednostkowa i prototypy` / `małoseryjna (do 1 000 szt.)` / `średnioseryjna (1 000–100 000 szt.)` / `masowa (powyżej 100 000 szt.)``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Procesy dodatkowe

**Procesy wykończeniowe i dodatkowe**  
- Typ: `multi-select: `lakierowanie` / `tampodruk` / `sitodruk` / `zgrzewanie` / `klejenie` / `montaż` / `pakowanie` / `znakowanie laserowe` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Certyfikaty

**Certyfikaty branżowe**  
- Typ: `multi-select: `ISO 9001` / `IATF 16949 (automotive)` / `ISO 13485 (medycyna)` / `BRC/IFS (opakowania food)` / `ISO 14001` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

---
## 5. Compounder
Producent kompoundów technicznych i mieszanek polimerowych. Ogniwo między dostawcą surowca a producentem wyrobu.

### Typ działalności

**Profil działalności**  
- Typ: `multi-select: `produkcja kompoundów technicznych` / `produkcja mieszanek specjalnych` / `przetwarzanie recyklatu na komponent` / `tolling (przerób na zlecenie)` / `mieszanki na zamówienie (custom compounding)``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Materiały bazowe

**Bazy polimerowe (surowce wejściowe)**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Przetwarza recyklat jako bazę**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Rosnące znaczenie — PPWR wymusza recyklat w kompoundach*  

### Modyfikacje i właściwości

**Typy modyfikacji / właściwości produktów**  
- Typ: `multi-select: `zbrojenie włóknem szklanym (GF)` / `zbrojenie włóknem węglowym (CF)` / `uniepalnienie (FR)` / `talcowanie` / `mineralne wypełnienie` / `modyfikacja udarności` / `antystatyczność` / `przewodność elektryczna` / `właściwości optyczne` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Kluczowy filtr — kupiec szuka konkretnej właściwości materiału*  

**Segmenty / aplikacje docelowe**  
- Typ: `multi-select: `automotive` / `elektronika` / `medycyna` / `budownictwo` / `opakowania` / `przemysł ogólny` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Forma i wolumen

**Forma produktu wyjściowego**  
- Typ: `multi-select: `granulat` / `proszek` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Minimalna ilość zamówienia (MOQ)**  
- Typ: `przedziały: `poniżej 100 kg` / `100–500 kg` / `500 kg–5 t` / `powyżej 5 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Kluczowa informacja dla mniejszych kupców*  

**Miesięczna przepustowość**  
- Typ: `przedziały: `poniżej 50 t` / `50–200 t` / `200–500 t` / `powyżej 500 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Certyfikaty

**Certyfikaty / dopuszczenia**  
- Typ: `multi-select: `REACH` / `RoHS` / `food-contact EC 10/2011` / `ISO 9001` / `IATF 16949` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

---
## 6. Producent dodatków, masterbatch i koncentratów

### Typ produktu

**Kategoria dodatku / produktu**  
- Typ: `multi-select: `masterbatch barwiący` / `masterbatch funkcyjny (additive MB)` / `komponent biały (white MB)` / `komponent czarny (black MB)` / `plastyfikator` / `stabilizator UV` / `stabilizator termiczny` / `antyoksydant` / `środek uniepalniający` / `środek spieniający` / `modyfikator udarności` / `środek antystatyczny` / `smar procesowy` / `środek poślizgowy` / `dodatek do recyklatu` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Lista będzie rozbudowywana wraz z rozwojem platformy i potrzebami dostawców*  

**Własna produkcja / dystrybucja**  
- Typ: `radio: `własna produkcja` / `autoryzowana dystrybucja` / `obydwa``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Bazy polimerowe

**Bazy polimerowe (do jakich materiałów)**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Masterbatch PE-HD nie działa w PA — kluczowy filtr techniczny*  

### Forma i wolumen

**Forma produktu**  
- Typ: `multi-select: `granulat` / `proszek` / `płyn` / `pasta` / `koncentrat ciekły``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Minimalna ilość zamówienia (MOQ)**  
- Typ: `przedziały: `poniżej 25 kg` / `25–100 kg` / `100–500 kg` / `powyżej 500 kg``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Dodatki to często małe ilości — MOQ decydujące dla małych firm*  

**Dozowanie na zamówienie (custom batch)**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Certyfikaty

**Dopuszczenia / certyfikaty**  
- Typ: `multi-select: `food-contact EC 10/2011` / `RoHS` / `REACH` / `NIR-detectable (do recyklingu)` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *NIR-detectable = nowy standard dla recyklingowalnych opakowań (PPWR 2026)*  

---
## 7. Recykler
Obejmuje recykling mechaniczny i chemiczny.

### Typ recyklingu

**Stosowana technologia recyklingu**  
- Typ: `multi-select: `recykling mechaniczny` / `recykling chemiczny (piroliza)` / `recykling chemiczny (depolimeryzacja)` / `recykling chemiczny (rozpuszczalnikowy)` / `recykling energetyczny``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Recykling chemiczny — rosnący segment w Polsce (piroliza PE/PP). Firmy coraz częściej łączą mechaniczny z chemicznym.*  

### Materiał wejściowy

**Materiał przyjmowany (frakcja)**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Najważniejszy filtr dla sprzedawców odpadów*  

**Forma przyjmowanego materiału**  
- Typ: `multi-select: `bele` / `luzem` / `shredd (płatki)` / `przemiał` / `folia` / `regranulat` / `odpady produkcyjne PIR (post-industrial)` / `odpady konsumenckie PCR (post-consumer)` / `mieszane``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Minimalna ilość przyjmowana (jednorazowo)**  
- Typ: `przedziały: `poniżej 100 kg` / `100–500 kg` / `500 kg–5 t` / `powyżej 5 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Produkt wyjściowy

**Materiał produkowany (frakcja)**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Kluczowy filtr dla kupców recyklatu*  

**Forma produktu wyjściowego**  
- Typ: `multi-select: `regranulat` / `granulat` / `shredd (płatki)` / `przemiał` / `proszek (pulwer)` / `aglomerat` / `olej pirolityczny``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Shredd/przemiał vs. regranulat — istotna różnica jakościowa i cenowa*  

**Klasa jakości produktu**  
- Typ: `multi-select: `przemysłowa` / `food-contact` / `medyczna``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Food-grade recyklat = premium — kluczowe dla opakowań PPWR*  

### Wolumen

**Miesięczna przepustowość (tony)**  
- Typ: `przedziały: `poniżej 50 t` / `50–200 t` / `200–500 t` / `powyżej 500 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Certyfikaty i regulacje

**Certyfikaty recyklatu**  
- Typ: `multi-select: `RecyClass` / `Cyclos-HTP` / `ISO 15270` / `inne` + wolne pole`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *RecyClass potwierdzony jako funkcjonujący na polskim rynku*  

**Wpis do rejestru BDO**  
- Typ: `tak / nie + numer rejestrowy`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Obowiązkowe dla podmiotów przetwarzających odpady w Polsce*  

### Logistyka

**Własny transport / odbiór odpadów**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Forma pakowania produktu**  
- Typ: `multi-select: `big-bag` / `worek 25 kg` / `luzem` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

---
## 8. Gospodarka odpadami
Regulowana działalność — inne zezwolenia niż recykler. Obejmuje zbieranie, sortowanie, przygotowanie do recyklingu.

### Typ działalności

**Rodzaj działalności**  
- Typ: `multi-select: `zbieranie odpadów tworzyw` / `sortowanie i segregacja` / `przygotowanie do recyklingu (belowanie, mielenie)` / `magazynowanie` / `transport odpadów` / `punkt skupu tworzyw` / `agregator odpadów` / `stacja przeładunkowa (RIPOK/PSZOK)``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Przyjmowane frakcje

**Frakcje tworzyw przyjmowane**  
- Typ: `multi-select z katalogu polimerów + `mix / frakcja mieszana``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Forma przyjmowanego materiału**  
- Typ: `multi-select: `luzem` / `bele` / `big-bag` / `worki` / `kontenery``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Źródło odpadów**  
- Typ: `multi-select: `od przedsiębiorstw (B2B)` / `od samorządów` / `z PSZOK` / `mieszane``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Regulacje i zezwolenia

**Wpis do rejestru BDO**  
- Typ: `tak / nie + numer rejestrowy`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **NIE**  
- Uwaga: *Obowiązkowe*  

**Decyzja środowiskowa / zezwolenie na przetwarzanie odpadów**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Odróżnia firmę z pozwoleniem od punktu skupu*  

### Zasięg i logistyka

**Zasięg zbierania / odbioru**  
- Typ: `multi-select: `lokalny (powiat/region)` / `regionalny (kilka województw)` / `ogólnopolski``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Własny transport / odbiór od klienta**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

---
## 9. Dostawca surowców pierwotnych
Autoryzowani dystrybutorzy i importerzy surowców virgin. Odróżniony od Tradera przez posiadanie własnego stocku i autoryzacji producenta.

### Model działalności

**Typ dostawcy**  
- Typ: `multi-select: `autoryzowany dystrybutor producenta` / `wyłączny importer` / `dystrybutor nieautoryzowany` / `własna produkcja + dystrybucja``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Zmienione z radio na multi-select. Autoryzowany dystrybutor (BASF, Sabic, LyondellBasell) = inny profil wiarygodności.*  

**Reprezentowane marki / producenci**  
- Typ: `wolne pole (multi-tag, np. BASF, Sabic, LyondellBasell, PKN Orlen, Borealis)`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Wyszukiwanie po marce producenta — potwierdzone jako potrzebne*  

### Oferta materiałowa

**Materiały w ofercie**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Forma surowca**  
- Typ: `multi-select: `granulat` / `regranulat` / `proszek` / `płyn` / `folia` / `arkusze` / `profile``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Dodano regranulat — część dostawców ma już recyklaty w ofercie*  

**Wyłącznie materiały virgin (pierwotne)**  
- Typ: `tak / nie`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Odróżnia od tradera który miesza virgin z recyklatem*  

### Warunki handlowe

**Dostępność magazynowa (materiał od ręki)**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Minimalna ilość zamówienia (MOQ)**  
- Typ: `przedziały: `poniżej 500 kg` / `500 kg–5 t` / `5–25 t` / `powyżej 25 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Własny transport / dostawa do klienta**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Zasięg

**Import bezpośredni**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

---
## 10. Trader
Handel tworzywami na własny rachunek. Posiada własny stock — to odróżnia go od Brokera.

### Profil handlowy

**Typ handlowanego materiału**  
- Typ: `multi-select: `surowce pierwotne (virgin)` / `recyklat` / `regranulat` / `odpady tworzyw` / `kompoundy` / `off-spec` / `nadwyżki produkcyjne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Multi-select — trader zazwyczaj łączy kilka typów*  

**Własny stock / magazyn**  
- Typ: `tak / nie`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Trader z magazynem ≠ broker — kluczowe rozróżnienie*  

### Oferta materiałowa

**Materiały w aktywnym handlu**  
- Typ: `multi-select z katalogu polimerów`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Forma materiału**  
- Typ: `multi-select: `granulat` / `regranulat` / `przemiał` / `aglomerat` / `proszek` / `bele` / `luzem` / `folia` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Warunki handlowe

**Minimalna ilość zamówienia (MOQ)**  
- Typ: `przedziały: `poniżej 500 kg` / `500 kg–5 t` / `5–25 t` / `powyżej 25 t``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Handel spot (jednorazowe partie)**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Kontrakty stałe (regularne dostawy)**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Regulacje (jeśli dotyczy)

**Wpis do rejestru BDO**  
- Typ: `tak / nie + numer rejestrowy`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Wymagane jeśli trader obraca odpadami tworzyw. Przy surowcach virgin lub recyklacie (nie odpadach) — BDO niewymagane.*  

### Zasięg

**Handel krajowy / eksport / import**  
- Typ: `multi-select: `rynek krajowy` / `eksport UE` / `eksport poza UE` / `import``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

---
## 11. Broker
Pośrednictwo handlowe bez własnego stocku. Kluczowa różnica wobec Tradera: broker nie trzyma towaru.

### Profil działalności

**Typ pośrednictwa**  
- Typ: `multi-select: `pośrednictwo w handlu surowcami virgin` / `pośrednictwo w handlu recyklatem` / `pośrednictwo w obrocie odpadami tworzyw` / `pośrednictwo w handlu maszynami i urządzeniami` / `kojarzenie kupujących i sprzedających (bez własnego stocku)` / `doradztwo i sourcing``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Dodano pośrednictwo w handlu maszynami — realna rola na rynku*  

**Własny stock / magazyn**  
- Typ: `tak / nie — oczekiwana odpowiedź: NIE`  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Jeśli firma ma własny stock → powinna wybrać kategorię Trader*  

### Specjalizacja materiałowa

**Materiały / produkty w których specjalizuje się broker**  
- Typ: `multi-select z katalogu polimerów + `maszyny i urządzenia` + `kompoundy` + `dodatki i masterbatch``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Typ materiału / produktu**  
- Typ: `multi-select: `surowce pierwotne` / `recyklat` / `odpady tworzyw` / `kompoundy` / `dodatki i masterbatch` / `maszyny nowe` / `maszyny używane` / `off-spec i nadwyżki``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Zasięg

**Zasięg geograficzny pośrednictwa**  
- Typ: `multi-select: `rynek krajowy` / `UE` / `poza UE``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Polscy brokerzy recyklatu aktywnie eksportują do Azji*  

### Regulacje

**Wpis do rejestru BDO (jeśli pośredniczy w odpadach)**  
- Typ: `tak / nie + numer rejestrowy`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *BDO wymagane przy pośrednictwie w obrocie odpadami. Przy surowcach virgin i maszynach — niewymagane.*  

---
## 12. Maszyny i urządzenia

### Typ maszyn i urządzeń

**Kategoria oferowanych maszyn**  
- Typ: `multi-select: `wtryskarki` / `wytłaczarki` / `linie blow moulding` / `linie termoformowania` / `linie rotomoulding` / `linie recyklingu (mycie, granulacja)` / `granulatory` / `rozdrabniarki` / `kruszarki` / `mieszarki i suszarki` / `chillery i systemy chłodzenia` / `transport pneumatyczny` / `dozowniki i mieszalniki grawimetryczne` / `roboty i automatyzacja` / `systemy wizyjne i kontrola jakości` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Lista będzie ewoluowała z czasem*  

**Stan maszyn**  
- Typ: `multi-select: `nowe` / `używane` / `odnowione (refurbished)``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

**Reprezentowane marki**  
- Typ: `wolne pole (multi-tag, np. Engel, Arburg, KraussMaffei, Erema, Zerma, Herbold)`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Usługi posprzedażowe

**Serwis i utrzymanie ruchu (UR)**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Części zamienne i eksploatacyjne**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Instalacja i uruchomienie**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

**Szkolenia operatorów i technologów**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Finansowanie

**Finansowanie / leasing**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  
- Uwaga: *Nie jest istotnym filtrem wyszukiwania — widoczne na profilu, niefiltrowane*  

---
## 13. Komponenty i części zamienne
Obejmuje produkcję form wtryskowych, części zamiennych do maszyn i oprzyrządowania.

### Typ działalności

**Co oferuje firma**  
- Typ: `multi-select: `produkcja form wtryskowych` / `naprawa i serwis form wtryskowych` / `produkcja części zamiennych do maszyn przetwórczych` / `produkcja oprzyrządowania i uchwytów` / `dystrybucja części i podzespołów` / `produkcja gorących kanałów` / `produkcja ślimaków i cylindrów` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Formy wtryskowe (jeśli dotyczy)

**Max gabaryty formy (oś X lub Y)**  
- Typ: `przedziały: `poniżej 500 mm` / `500–1000 mm` / `1000–2000 mm` / `powyżej 2000 mm``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Wypełnić jeśli firma produkuje formy*  

**Max waga formy**  
- Typ: `przedziały: `poniżej 500 kg` / `500–2000 kg` / `powyżej 2000 kg``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Gorące kanały**  
- Typ: `tak / nie + marki (np. Husky, Mold-Masters, HASCO)`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Typowy czas realizacji formy**  
- Typ: `przedziały: `poniżej 6 tyg.` / `6–12 tyg.` / `12–20 tyg.` / `powyżej 20 tyg.``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Części zamienne (jeśli dotyczy)

**Typy maszyn dla których dostarcza części**  
- Typ: `multi-select: `wtryskarki` / `wytłaczarki` / `blow moulding` / `linie recyklingu` / `granulatory` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Wypełnić jeśli firma dostarcza części zamienne*  

**Marki maszyn obsługiwane**  
- Typ: `wolne pole (multi-tag)`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

---
## 14. Technologia i IT
Dostawcy oprogramowania, automatyzacji i rozwiązań technologicznych dla branży tworzyw.

### Typ rozwiązania

**Kategoria oferowanych rozwiązań**  
- Typ: `multi-select: `oprogramowanie MES` / `oprogramowanie ERP dla przetwórstwa tworzyw` / `oprogramowanie WMS (magazyn)` / `systemy kontroli jakości i wizyjne` / `automatyzacja i robotyzacja linii` / `IIoT i monitoring maszyn` / `oprogramowanie do projektowania form (CAD/CAM/CAE)` / `symulacja wtrysku (Moldflow i in.)` / `systemy ważenia i dozowania` / `inne``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  
- Uwaga: *Lista będzie ewoluowała z czasem*  

**Model dostarczenia**  
- Typ: `multi-select: `SaaS` / `on-premise` / `wdrożenie na zamówienie` / `integracja z istniejącymi systemami``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Branże obsługiwane

**Segmenty branżowe**  
- Typ: `multi-select: `przetwórstwo tworzyw (ogólnie)` / `recykling` / `automotive` / `opakowania` / `medycyna` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

### Usługi

**Wdrożenie i integracja**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Serwis i wsparcie techniczne**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Szkolenia**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

---
## 15. Laboratorium i B+R

### Typ działalności

**Profil działalności**  
- Typ: `multi-select: `usługi laboratoryjne (badania zlecone)` / `własne laboratorium zakładowe` / `instytut badawczy` / `centrum B+R przy uczelni` / `prywatne centrum B+R` / `certyfikacja i atestacja materiałów``  
- Obowiązkowe: **TAK** | Wyszukiwalne: **TAK**  

### Usługi laboratoryjne

**Typy badań oferowanych**  
- Typ: `multi-select: `badania mechaniczne (wytrzymałość, udarność, twardość)` / `badania termiczne (DSC, TGA, HDT/Vicat)` / `badania reologiczne (MFI, lepkość)` / `badania chemiczne i skład` / `identyfikacja tworzyw (FTIR, Raman, DSC)` / `badania migracji i food-contact` / `badania starzenia i odporności na UV` / `badania elektryczne i elektrostatyczne` / `badania płomienności i palności` / `badania środowiskowe (woda, gleba)` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Akredytacja PCA**  
- Typ: `tak / nie + numer akredytacji`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *Osobny filtr wyszukiwania. Wyniki akredytowane wymagane w przetargach i kontraktach B2B.*  

**Jednorazowe zlecenia**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Obsługa seryjna / umowy stałe**  
- Typ: `tak / nie`  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Typowy czas realizacji raportu**  
- Typ: `przedziały: `poniżej 3 dni roboczych` / `3–7 dni` / `1–3 tygodnie` / `powyżej 3 tygodni``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **NIE**  

### Działalność B+R

**Zakres prac B+R**  
- Typ: `multi-select: `opracowanie nowych receptur i materiałów` / `optymalizacja parametrów przetwórstwa` / `testy aplikacyjne nowych materiałów` / `projekty z dofinansowaniem (NCBiR, Horyzont)` / `współpraca z uczelniami i instytutami` / `inne``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  

**Zaplecze naukowe / afiliacja**  
- Typ: `radio: `uczelnia` / `instytut badawczy (IMPiB, ICSO i in.)` / `firma prywatna` / `brak formalnej afiliacji``  
- Obowiązkowe: **NIE** | Wyszukiwalne: **TAK**  
- Uwaga: *IMPiB Bydgoszcz i ICSO Blachownia — kluczowe instytuty branżowe w Polsce*  

---
## 16. Katalog polimerów
Lista zarządzana przez admina polyGo. Firmy wybierają materiały z listy. Właściciel firmy może zaproponować brakujący polimer — po zatwierdzeniu przez admina staje się dostępny dla wszystkich.

Lista alfabetyczna — 103 pozycje:

| # | Kod | Opcje / modyfikatory |
|---|-----|----------------------|
| 1 | `ABS` | Blend |
| 2 | `Additive` | CF - Carbon Fiber |
| 3 | `ASA` | Crosslinked |
| 4 | `Bio` | FR - Flame Retardant |
| 5 | `CA` | GF - Glass Fiber |
| 6 | `CAB` | High Heat |
| 7 | `Cellulose` | High Impact |
| 8 | `COC` | Impact Modified |
| 9 | `Copolyester` | Low Friction |
| 10 | `CP` | Mineral Filled |
| 11 | `CPVC` | Talc Filled |
| 12 | `EPDM` | — |
| 13 | `EPE` | — |
| 14 | `EPP` | — |
| 15 | `EPS` | — |
| 16 | `ETFE` | — |
| 17 | `EVA` | — |
| 18 | `EVOH` | — |
| 19 | `FEP` | — |
| 20 | `Filler` | — |
| 21 | `HIPS` | — |
| 22 | `Ionomer` | — |
| 23 | `LCP` | — |
| 24 | `MABS` | — |
| 25 | `Masterbatch` | — |
| 26 | `OTHERS` | — |
| 27 | `PA` | — |
| 28 | `PA 10` | — |
| 29 | `PA 11` | — |
| 30 | `PA 12` | — |
| 31 | `PA 4.6` | — |
| 32 | `PA 6` | — |
| 33 | `PA 6.10` | — |
| 34 | `PA 6.12` | — |
| 35 | `PA 6.6` | — |
| 36 | `PA amorph` | — |
| 37 | `PAI` | — |
| 38 | `PAN` | — |
| 39 | `PAR` | — |
| 40 | `PARA` | — |
| 41 | `PB` | — |
| 42 | `PBT` | — |
| 43 | `PC` | — |
| 44 | `PCL` | — |
| 45 | `PCT` | — |
| 46 | `PCTFE` | — |
| 47 | `PCTG` | — |
| 48 | `PE` | — |
| 49 | `PE-HD` | — |
| 50 | `PE-LD` | — |
| 51 | `PE-LLD` | — |
| 52 | `PE-MD` | — |
| 53 | `PEEK` | — |
| 54 | `PEI` | — |
| 55 | `PEKK` | — |
| 56 | `PES (PESU)` | — |
| 57 | `PET` | — |
| 58 | `PET-A` | — |
| 59 | `PET-C` | — |
| 60 | `PET-G` | — |
| 61 | `PFA` | — |
| 62 | `PGA` | — |
| 63 | `PHB` | — |
| 64 | `PI` | — |
| 65 | `PLA` | — |
| 66 | `PMMA` | — |
| 67 | `PMP` | — |
| 68 | `POM` | — |
| 69 | `PP` | — |
| 70 | `PP-Copo` | — |
| 71 | `PP-Homo` | — |
| 72 | `PPA` | — |
| 73 | `PPE` | — |
| 74 | `PPO` | — |
| 75 | `PPS` | — |
| 76 | `PPSU` | — |
| 77 | `PS` | — |
| 78 | `PSU` | — |
| 79 | `PTFE` | — |
| 80 | `PUR` | — |
| 81 | `PVB` | — |
| 82 | `PVC` | — |
| 83 | `PVDC` | — |
| 84 | `PVDF` | — |
| 85 | `SAN` | — |
| 86 | `SBR` | — |
| 87 | `SBS` | — |
| 88 | `SEBS` | — |
| 89 | `Silikon` | — |
| 90 | `SMA` | — |
| 91 | `SMMA` | — |
| 92 | `SRP` | — |
| 93 | `TEEE` | — |
| 94 | `TPC` | — |
| 95 | `TPE` | — |
| 96 | `TPI` | — |
| 97 | `TPO` | — |
| 98 | `TPS` | — |
| 99 | `TPU` | — |
| 100 | `TPV` | — |
| 101 | `UHMWPE` | — |
| 102 | `XLPE` | — |
| 103 | `XPS` | — |

---
## 17. Decyzje produktowe — podsumowanie
Kluczowe decyzje podjęte podczas tworzenia specyfikacji (wersje v1–v3).

| Obszar | Decyzja |
|--------|--------|
| **NIP** | Obsługa formatu PL-prefix (PL1112223344) dla firm zagranicznych zarejestrowanych w Polsce |
| **Adres** | Osobne pola na nr budynku i nr lokalu we wszystkich adresach |
| **Zasięg działalności** | Pole obowiązkowe — ważny filtr dla kupców |
| **Certyfikaty** | Filtr wyszukiwania; dodano RecyClass; uwaga o wymogu certyfikatu od partnera |
| **Warunki płatności** | USUNIĘTE z formularza — wrażliwe handlowo, nieadekwatne na profilu publicznym |
| **Kategoria branżowa** | Multi-select — firmy działają w kilku branżach jednocześnie |
| **Compounder** | Dodana jako osobna kategoria — ogniwo między dostawcą surowca a producentem wyrobu |
| **Broker** | Osobna kategoria; rozszerzony o pośrednictwo w handlu maszynami |
| **Trader — BDO** | Pole BDO dodane jako nieobowiązkowe — wymagane tylko przy obrocie odpadami |
| **Recykler — nomenklatura** | Shredd (płatki), przemiał, aglomerat, proszek (pulwer) zamiast 'flakes' |
| **Dostawca surowców — Typ** | Zmieniony z radio na multi-select |
| **Leasing maszyn** | Widoczne na profilu, ale NIE jest filtrem wyszukiwania |
| **Katalog polimerów** | Lista alfabetyczna — prosta i przewidywalna; 103 pozycje |
| **Spot offer (Trader/Broker)** | Odłożone do v2 — na start nieimplementowane |
| **Wiele adresów** | Obsługa wielu lokalizacji / oddziałów |

---
*Dokument wygenerowany z polygo_formularz_rejestracji_v3.xlsx — czerwiec 2026*
