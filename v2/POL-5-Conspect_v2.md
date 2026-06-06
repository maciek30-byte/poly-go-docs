# polyGo — Conspect v2

## Co to jest

polyGo to narzędzie do nawiązywania i utrzymywania kontaktów handlowych B2B. Jego celem jest zwiększanie zasięgów firm i produktywności pracowników. Nie jest to marketplace. Jest to zamknięta platforma dla sektora tworzyw sztucznych — łącząca zweryfikowany katalog firm z wbudowanym komunikatorem. Każda firma wchodzi wyłącznie po ręcznej weryfikacji przez założyciela — to jest moat produktu.

## Zasada nadrzędna

Firma niezweryfikowana nie jest nigdzie widoczna i nigdy nie pojawia się w żadnym widoku.

## Role

| Rola | Odpowiedzialność |
|---|---|
| **Platform Administrator** | Weryfikuje firmy (NIP/KRS), aktywuje lub odrzuca, blokuje konta |
| **Company Owner / Admin firmy** | Akceptuje zaproszenie, wypełnia profil, zaprasza pracowników, dezaktywuje pracowników, widzi historię czatów byłych pracowników (tylko po dezaktywacji — nie w trakcie zatrudnienia) |
| **Employee / Użytkownik** | Szuka firm, pisze na czacie, wymienia PDFy, dodaje do ulubionych |

Rejestracja wyłącznie przez zaproszenie — brak publicznego formularza.

---

## DEMO — jeden przepływ end-to-end: znajdź firmę → napisz do niej

| Moduł | Zakres |
|---|---|
| **Onboarding** | Zaproszenie e-mail → rejestracja Ownera → weryfikacja NIP/KRS przez admina → aktywacja firmy |
| **Profil firmy** | Nazwa, NIP, kategoria działalności, wielopoziomowe adresy (rejestracyjny + siedziba + oddziały) |
| **Zarządzanie pracownikami** | Zapraszanie przez e-mail, podział na Admin / Użytkownik, dezaktywacja konta + retencja historii czatu dla Ownera |
| **Wyszukiwarka firm** | Filtr: typ działalności; widoczne tylko firmy `activated` |
| **Komunikator** | 1:1 między firmami oraz wewnątrz tej samej firmy; tekst + PDF ≤ 10 MB; dane personalne (w tym telefon) widoczne dla innych użytkowników |
| **Ulubione** | Gwiazdkowanie firm i kontaktów — wchodzi do Demo jeśli koszt wdrożenia akceptowalny |
| **Personalizacja** | Wersja minimalna: zarządzanie profilem użytkownika i profilu firmy |
| **Landing page** | Już istnieje — wymaga dostosowania do aktualnej wersji produktu |

## MVP — Demo + poniższe

| Moduł | Zakres |
|---|---|
| **Rozbudowany profil firmy** | Zdjęcia, opis/misja, dokumenty firmowe, certyfikaty |
| **Formularze wg typu działalności** | Każdy typ działalności ma swoje predefiniowane pola przy rejestracji; wybór polimerów tylko dla wybranych typów (szczegóły: `polygo_formularz_rejestracji_v3.md`) |
| **Kontrola widoczności profilu** | Pełna / ukryta + system zaproszeń z kodem polecającym |
| **Read receipts + push notifications** | Potwierdzenia odczytu wiadomości; powiadomienia push w przeglądarce |
| **Centrum powiadomień** | Dzwoneczek z powiadomieniami systemowymi — *⚠️ do decyzji: Demo czy MVP?* |

## v2+ — dalszy rozwój

| Moduł | Uwaga |
|---|---|
| **Tablica Giełdowa** | Ogłoszenia "Kupię", "Usługi" — koncepcja wymiany informacji do doprecyzowania |
| **Obserwacja rynku** | Śledzenie aktywności wybranych partnerów |
| **Propozycja nowego polimeru** | Firma proponuje, admin zatwierdza |
| **Magazyn / Produkcja** | Alternatywne podejście do prezentacji oferty — stany magazynowe jako forma marketplace |
| **Zarządzanie transakcjami i obieg dokumentów** | Śledzenie statusu dealów, repozytorium dokumentów |
| **Czat grupowy** | Multi-party threads |
| **Aplikacja mobilna** | iOS / Android |

---

## Tech

React SPA (Vite) + Supabase (Postgres, auth, realtime, storage) + Cloudflare Pages — solo, after-hours build.
