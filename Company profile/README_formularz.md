# polyGo — Specyfikacja formularza rejestracji firm

> **Dla:** Maciek  
> **Od:** Grzegorz  
> **Data:** czerwiec 2026  
> **Plik specyfikacji:** `polygo_formularz_rejestracji_v3.md`

---

## Co tu znajdziesz

Ten dokument to kompletna specyfikacja **formularza rejestracji firmy** w polyGo — wynik kilku sesji product design między mną a Claude.

Zawiera:
- pola wspólne dla wszystkich firm (NIP, adres, widoczność profilu itd.)
- 12 kategorii branżowych z polami specyficznymi dla każdej
- katalog 103 polimerów (lista alfabetyczna z modyfikatorami)
- wszystkie podjęte decyzje produktowe z uzasadnieniem

---

## Jak czytać specyfikację

### Każde pole ma cztery atrybuty

```
**Nazwa pola**
- Typ: `multi-select: opcja A / opcja B / opcja C`
- Obowiązkowe: TAK | Wyszukiwalne: TAK
- Uwaga: kontekst biznesowy lub techniczna pułapka
```

- **Typ** — co budujesz: `tekst`, `dropdown`, `multi-select`, `radio`, `tak / nie`, `upload`, `liczba`
- **Obowiązkowe** — czy pole blokuje submit formularza
- **Wyszukiwalne** — czy pole trafia do indeksu i pojawia się jako filtr w katalogu firm
- **Uwaga** — rzeczy, które mogą Cię zaskoczyć; czytaj zanim zaczniesz kodować

### Logika warunkowa

Formularz działa dwupoziomowo:

1. **Pola wspólne** — wypełnia każda firma
2. **Pola branżowe** — odsłaniane dynamicznie po wyborze kategorii

Kategoria branżowa to **multi-select** — firma może wybrać kilka. Jeśli wybierze np. `Producent` i `Recykler`, dostaje pola z obydwu sekcji.

### Widoczność profilu

Dwa tryby — ważne dla RLS w Supabase:

| Tryb | Co widzi inny zalogowany użytkownik |
|------|--------------------------------------|
| **Pełna widoczność** | Wszystkie dane + dostęp do komunikatora |
| **Brak widoczności** | Tylko nazwa, logo, opis, zdjęcia — komunikator zablokowany |

Przy braku widoczności inni mogą wysłać **Zaproszenie** z opcjonalnym **Kodem polecającym**.

---

## Katalog polimerów

Lista 103 pozycji — zarządzana przez admina polyGo, nie przez użytkowników.

Firma wybiera z listy. Jeśli brakuje pozycji — właściciel konta proponuje, admin zatwierdza, wtedy pozycja staje się globalnie dostępna.

Kolumna `Opcje / modyfikatory` pokazuje warianty danego polimeru (GF, FR, High Impact itd.) — to informacja do budowy subkategorii lub tagów przy materiale.

---

## Decyzje, które wpływają na model danych

Sekcja 17 w specyfikacji zbiera wszystkie decyzje produktowe. Najważniejsze z perspektywy backendu:

| Decyzja | Implikacja |
|---------|-----------|
| Wiele adresów prowadzenia działalności | Relacja 1:N firma → adresy |
| Kategoria branżowa = multi-select | Tabela junction firma ↔ kategoria |
| BDO w Traderze i Brokerze — nieobowiązkowe | Pole nullable, warunkowo wymagane |
| Wyszukiwalne = TAK | Pole musi być indeksowane / dostępne przez RLS dla zalogowanych |
| Widoczność profilu | RLS policy na poziomie firmy |
| Certyfikaty jako filtr | Tabela junction firma ↔ certyfikat |

---

## Czego tu nie ma

To jest specyfikacja **formularza rejestracji** — nie pokrywa:
- przepływu weryfikacji przez admina (osobny temat)
- modelu danych pracowników (Employee)
- komunikatora
- logiki wyszukiwarki po stronie query

Te tematy możemy opracować osobno w tym samym formacie.

---

## Pytania

Jeśli coś jest niejasne lub widzisz konflikt z PRD — wróć do Grzegorza. Kilka otwartych kwestii oznaczonych w specyfikacji jako `będzie ewoluowało` (lista maszyn, lista dodatków) — traktuj je jako listy startowe do rozszerzenia.
