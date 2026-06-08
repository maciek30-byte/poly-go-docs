# POL-6 — Company Profile

> Odpowiedzi biznesowe do projektowania widoku profilu firmy.

---

## Architektura widoku

**Jedna strona czy zakładki?**

Nie znam się aż tak na UX/UI i dlatego mam tu dylemat do omówienia. Jedna strona scrollowana z kotwicami (anchor links) w nagłówku profilu będzie wyglądała nowocześnie. Ważne, żeby strony profili wszystkich firm miały ten sam schemat, bo to ułatwi przeszukiwanie serwisu. Użytkownik jednym spojrzeniem zeskanuje profil — nie musi klikać zakładek żeby dowiedzieć się czy firma jest odpowiednim partnerem.

Z drugiej strony dobrze byłoby mieć jednak chociaż dwie zakładki, gdzie użytkownik znajdzie od ręki wszystkie "Dane rejestrowe firmy" i adresy oraz "Listę pracowników" z przypisanym stanowiskiem i danymi kontaktowymi — opcja nawiązania rozmowy.

Zakładki fragmentują flow, ale z drugiej strony pozwalają przejść szybko do szczegółowych list danych, które będziemy mogli dowolnie modyfikować i rozbudowywać. Może miałbyś na to jakiś pomysł?

---

**Co jest najważniejsze "above the fold"?**

W pierwszym rzędzie widoczności (bez scrollowania):

- Logo + Nazwa firmy + rok założenia
- Kategorie działalności (może coś w stylu tagi/badges — jakieś wyróżniki, które pozwolą szybko uzyskać odpowiedź, czy to firma dla danego użytkownika, który przegląda profil)
- Dwa przyciski CTA: **Napisz** (komunikator) + **Dodaj do ulubionych** (gwiazdka)

Jeśli uruchomimy ten rozbudowany profil firmy to może Top 5 tego co firma robi — to Owner zdecyduje co tam będzie, reszta ukryta za "pokaż wszystkie".

---

## Zawartość i dane

**Jakie pola w nagłówku (wizytówce)?**

- Logo firmy
- Nazwa firmy
- Kategorie działalności (tagi)
- Rok założenia
- Certyfikaty (ikony / tagi — np. ISO 9001, IATF)

---

**Długi opis "O firmie" czy twarde parametry techniczne?**

Obydwa — ale w oddzielnych sekcjach:

**Sekcja 1 — Opis firmy:** swobodny tekst do 600 znaków. Firma pisze własnymi słowami czym się zajmuje, co ją wyróżnia.

**Sekcja 2 — Parametry techniczne:** pola strukturyzowane zależne od wybranych kategorii działalności (np. dla Producenta: technologie przetwórstwa, siła zwarcia maszyn, segmenty rynku; dla Recyklera: frakcje przyjmowane, forma produktu, przepustowość).

---

**Pliki do pobrania i galeria zdjęć?**

Tak — obydwa.

- **Galeria zdjęć:** do 5 zdjęć (hala produkcyjna, maszyny, magazyn). Widoczna na profilu dla wszystkich zalogowanych.
- **Dokumenty do pobrania:** do 5 plików PDF, max 10 MB każdy (certyfikaty jakości, karty technologiczne, prezentacja firmy). Dostępne po kliknięciu przycisku "Pobierz" przy każdym pliku.

---

## Akcje i interakcje

**Główne CTA — czy dodajemy RFQ?**

Nie — RFQ poza zakresem Demo i MVP.

Dwa przyciski CTA wystarczą:

- **Napisz** — przenosi do listy pracowników z nazwami stanowisk, gdzie możemy otworzyć komunikator 1:1 z wybranym pracownikiem firmy
- **Dodaj do ulubionych** — gwiazdka, toggle

Komunikator jest kanałem do wysłania zapytania ofertowego — nie potrzebujemy osobnego formularza RFQ w Demo/MVP.

---

**Akcje poboczne?**

Te CTA, które wspomnieliśmy, chyba wystarczą na start, bo np.:

- **Zgłoś nieaktualne dane** — nie wiem jak miałoby to działać, ale raczej nie. Czy zgłaszałby to ktoś z zewnątrz — to pole do nadużyć. Owner może sam zmienić swoje dane.
- **Udostępnij link do profilu** — można zaimplementować jako "Skopiuj link" (dla zalogowanych), który użytkownicy mogą sobie podawać przez komunikator, aby polecać firmy. Bez wartości dla osób spoza platformy.
- **Pobierz wizytówkę** = dodaj do ulubionych. Wolałbym, aby całe "życie ewoluowało" u nas. Nie ułatwiałbym kopiowania danych na zewnątrz ;]

---

*Dokument wygenerowany na podstawie POL-6 · czerwiec 2026*
