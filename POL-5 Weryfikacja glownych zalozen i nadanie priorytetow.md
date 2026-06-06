# Weryfikacja glownych zalozen i nadanie priorytetow

Tutaj wypisalem glowne funkcjonalnosci z paczkek z dokumentami ktore mi wyslales.

Twoje zadanie to

*  sprawdzenie czy wszystko sie zgadza, czy czegos nie brakuje? czy cos jest za duzo .
* Zakwalifikowanie funkcjonalnosci (dodanie nowych, jesli trzeba)



Bedziemy budowac 2 wersje aplikacji 

(mozemy rozwazyc 3 cia wersje, jesli bedzie taka potrzeba)

***1 Demo:***

* tutaj klasyfikujesz wszystkie rzeczy ktore MUSZA OD RAZU znalezc sie w aplikacji zeby miala wartosc biznesowa i gdzie bedzie mozna ja pokazywac firmom

2 MVP

* tutaj wszystko co musimy dorobic aby podniesc komfort uzytwkonikow, ale aplikacja bedzie dzialac bez tego

Przyklad 

Komunikacja i Budowanie Relacjii musi byc w DEMO

Tablica Gieldowa moze isc do MVP

1\. Zarządzanie Profilem Firmy i Tożsamością

To fundament systemu, budujący wiarygodność na rynku polimerów.

* **Rozbudowana Wizytówka Firmy:** Użytkownik w procesie rejestracji tworzy profil, wprowadzając dane rejestrowe, historię i misję. Firma określa swoją kategorię działalności (np. Producer, Recycler, Trader) oraz dokładnie wybiera polimery, którymi się zajmuje z predefiniowanej listy.
* **Wielopoziomowe Adresy:** System obsługuje różne typy lokalizacji dla jednego podmiotu: adres rejestracyjny, adres głównej siedziby oraz adresy poszczególnych oddziałów/placówek.
* **Precyzyjna Kontrola Widoczności (Prywatność):** Firma sama decyduje, jak dużo informacji ujawnia. Opcja "Pełna widoczność" udostępnia dane rejestrowe, kontaktowe i pozwala na bezpośredni kontakt. Opcja "Brak widoczności" ukrywa te dane przed ogółem, pozostawiając tylko logo i nazwę; do nawiązania relacji wymagane jest wysłanie specjalnego zaproszenia (z opcją podania kodu polecającego).
* **Zarządzanie Uprawnieniami (Role):** Pierwszy użytkownik rejestrujący firmę staje się jej Administratorem. Architektura bazy pozwala na zapraszanie kolejnych pracowników, przypisywanie ich do działów, nadawanie im stanowisk i ról, które warunkują, do jakich sekcji aplikacji mają dostęp.

### 2\. Tablica Giełdowa (Marketplace)

Moduł, który dynamizuje rynek i pozwala na szybkie reagowanie na potrzeby.

* **Sekcje Ogłoszeniowe:** W sitemapie znajduje się główny moduł "Tablica", który zawiera kategorie takie jak "Kupię" oraz "Usługi". Umożliwia to firmom szybkie informowanie rynku o swoim bieżącym zapotrzebowaniu na surowiec lub oferowanie wolnych mocy przerobowych/usług transportowych.

### 3\. Komunikacja i Budowanie Relacji (CRM)

Wewnętrzne narzędzia zastępujące e-maile i rozproszone notesy.

* **Ogólna Baza Firm:** Wyszukiwarka pozwalająca na przeglądanie wszystkich zarejestrowanych podmiotów i docieranie do nowych dostawców lub odbiorców.
* **Wewnętrzny Komunikator:** Narzędzie do bezpośrednich, prywatnych rozmów pomiędzy pracownikami różnych firm (przy zachowaniu zasad widoczności).
* **Zarządzanie Kontrahentami (Ulubione):** Użytkownicy mogą zapisywać firmy oraz konkretnych pracowników innych firm do specjalnych folderów ("Ulubione firmy", "Ulubione kontakty").
* **Obserwacja Rynku:** Funkcja "Obserwowane pozycje innych kontrahentów", pozwalająca na śledzenie aktywności lub ofert ważnych dla użytkownika partnerów.

### 4\. Operacje i Logistyka (Magazyn / Produkcja)

Mini-system klasy ERP zaszyty w aplikacji do zarządzania przepływem towarów.

* **Mój Magazyn i Planowanie:** Zalogowany pracownik (z odpowiednimi uprawnieniami) ma dostęp do modułu zarządzania produkcją i własnym magazynem firmy.
* **Współdzielenie Zasobów:** System oferuje zakładkę "Udostępnione z magazynu", co oznacza, że firma może wystawić część swoich stanów magazynowych na widok publiczny lub dla wybranych partnerów.

### 5\. Zarządzanie Transakcjami i Obieg Dokumentów

Ustrukturyzowanie formalności po ustaleniach na czacie.

* **Panel Transakcji:** Dedykowane miejsce do śledzenia statusu dealów. Sitemap dzieli to na transakcje "W trakcie realizacji", "Zakończone" oraz "Archiwum".
* **Centralne Repozytorium Dokumentów:** Miejsce do zarządzania dokumentacją firmową i transakcyjną. Użytkownik ma podgląd na "Dokumenty firmy" (które można wgrać już podczas rejestracji) oraz sekcje na pliki "Do wydania", "Otrzymane", i "Archiwum".

### 6\. Doświadczenie Użytkownika (UX) i Powiadomienia

Elementy spinające aplikację w nowoczesny produkt SaaS.

* **Landing Page:** Zewnętrzne widoki dla niezalogowanych, w tym strona główna, cennik (aplikacja docelowo będzie monetyzowana) oraz formularz kontaktowy do twórców.
* **Centrum Powiadomień:** Użytkownik ma własną sekcję powiadomień systemowych (tzw. dzwoneczek) o nowych zdarzeniach, wiadomościach czy ofertach.
* **Personalizacja:** Panel ustawień dający możliwość zarządzania profilem użytkownika, profilami firmy oraz preferencjami interfejsu (np. opcja włączenia "Trybu ciemnego").

## Metadata
- URL: [https://linear.app/poly-go-biznes/issue/POL-5/weryfikacja-glownych-zalozen-i-nadanie-priorytetow](https://linear.app/poly-go-biznes/issue/POL-5/weryfikacja-glownych-zalozen-i-nadanie-priorytetow)
- Identifier: POL-5
- Status: Todo
- Priority: Urgent
- Assignee: Grzegorz Suchocki
- Labels: Feature
- Created: 2026-06-04T22:54:22.940Z
- Updated: 2026-06-04T22:56:08.414Z