# Sygnały — brief dla Macka
> czerwiec 2026 | pełna spec: `sygnaly-feature-spec-v1.md`

---

## Dlaczego Sygnały, nie marketplace

Typowy marketplace branżowy ma trzy problemy strukturalne: nieaktualne ogłoszenia, niezweryfikowane firmy i brak kontroli nad tym, kto widzi Twoje dane handlowe. Sprzedawca zapomina usunąć partię którą sprzedał trzy tygodnie temu. Kupujący nie wie czy firma po drugiej stronie w ogóle istnieje. A Twój konkurent widzi dokładnie co kupujesz i w jakiej ilości.

Sygnały rozwiązują to inaczej, bo opierają się na fundamencie który polyGo już ma: zweryfikowanej sieci.

Sygnał MAMY od recyklera oznacza że to **prawdziwy, zweryfikowany recykler** — nie bot, nie lead generator, nie firma-widmo. Świeżość jest strukturalna — sygnał wygasa automatycznie, więc nieaktualne ogłoszenia znikają bez udziału użytkownika. Dystrybucja jest intencjonalna — firma sama decyduje kto widzi jej stan magazynowy i potrzeby zakupowe, więc konkurencja nie dostaje darmowego wglądu w Twoje operacje.

Dla polyGo jako produktu Sygnały mają jeszcze jeden efekt: zamieniają katalog firm (który przeglądasz raz) w **codzienny nawyk**. Feed rynkowych sygnałów to powód żeby zalogować się rano i sprawdzić co nowego — tak jak przegląda się branżowe newsy. To kluczowe dla retencji użytkowników w modelu SaaS.

Sygnały to nie marketplace. To rynkowa komunikacja w zamkniętej, zaufanej sieci.

---

## Co to jest

Funkcja v2, **nie MVP**. Firmy na polyGo mogą publikować krótkie komunikaty rynkowe:
- **MAMY** — mam coś do sprzedania / do oddania
- **SZUKAMY** — szukam czegoś do kupienia / pozyskania

To **nie jest marketplace**. Brak cen, brak transakcji, brak publicznych listingów. Cała rozmowa handlowa odbywa się przez istniejący komunikator polyGo.

---

## Dlaczego v2, nie MVP

Feed jest pusty i bezużyteczny przy < 80 firmach. Uruchamiamy Sygnały gdy osiągniemy ten próg. MVP zostaje skupione na rdzeniu: znajdź firmę → napisz do niej.

---

## Jak to działa (w skrócie)

1. Firma tworzy sygnał (MAMY lub SZUKAMY) + wypełnia formularz branżowy
2. Wybiera **kto zobaczy** sygnał: wszyscy / obserwujący / ulubione / wybrany segment / konkretne firmy
3. Sygnał pojawia się w **feedzie** u właściwych odbiorców
4. Odbiorca klika "Odpowiedz" → otwiera się komunikator z kontekstem sygnału

---

## Struktura formularza

Dwa modele:

**Materiałowy** (gałęzie 1–8): polimer z katalogu, forma, ilość, termin, transport, certyfikaty
→ Recykler, Producent, Compounder, Dodatki, Gospodarka odpadami, Surowce pierwotne, Trader, Broker

**Usługowy** (gałęzie 9–12): typ usługi, dostępność, liczba miejsc, zasięg realizacji
→ Maszyny, Komponenty, Technologia/IT, Laboratorium

Broker ma obowiązkowy znacznik **POŚREDNICTWO** na każdym sygnale — odbiorcy zawsze wiedzą z kim rozmawiają.

Maszyny do sprzedania może wystawić **każda firma**, nie tylko gałąź "Maszyny i urządzenia".

---

## Dystrybucja (kto widzi)

| Poziom | Kto |
|--------|-----|
| Wszyscy | wszystkie zweryfikowane firmy polyGo |
| Obserwujący | firmy które obserwują nadawcę |
| Ulubione | lista ulubionych nadawcy |
| Segment | nazwana lista kontaktów (np. "Klienci HDPE") |
| Wybrane firmy | ręcznie wskazane firmy |

Firma z profilem ukrytym nie może wybrać "Wszyscy".

---

## Powiadomienia push

- **Obserwuj firmę** → powiadomienie gdy opublikuje nowy sygnał
- **Alert materiałowy** → użytkownik ustawia kryteria (polimer, ilość, gałąź) i dostaje powiadomienie gdy pojawi się pasujący sygnał
- **Digest dzienny** → e-mail o 8:00 z listą nowych sygnałów pasujących do alertów

---

## Cykl życia sygnału

Sygnał wygasa po 30 dniach (domyślnie) lub w ustawionej dacie. 3 dni przed — przypomnienie o odnowieniu. Odnowienie jednym kliknięciem — nie wyzwala ponownych powiadomień jeśli treść się nie zmieniła.

---

## Co jest poza zakresem v2

Integracja z magazynem (auto-wygaśnięcie po wyprzedaniu), ceny na sygnale, publiczny feed bez logowania, alerty SMS, statystyki wyświetleń sygnału, klonowanie sygnałów.

---

## Decyzje produktowe — uzupełnione

| # | Pytanie | Decyzja |
|---|---------|---------|
| 1 | Limit aktywnych sygnałów na firmę? | **Start: 10.** Cel: ochrona feedu przed zdominowaniem przez jedną firmę gdy sieć jest mała. Docelowo cap zostanie zniesiony gdy sieć osiągnie dojrzałość (orientacyjnie 200+ aktywnych firm). |
| 2 | Admin polyGo widzi wszystkie sygnały? | **TAK** — pełna widoczność dla celów moderacji, włącznie z sygnałami ustawionymi na "Wybrane firmy". |
| 3 | Co dzieje się z sygnałami gdy firma zostaje zablokowana? | **Sygnały znikają z ekosystemu natychmiast** — zgodnie z zasadą: niezweryfikowana/zablokowana firma jest niewidoczna wszędzie, zawsze. |
