# polyGo w Linearze — jak z tego korzystać

Projekt: **polyGo MVP** → https://linear.app/poly-go/project/polygo-mvp-46ee88f1abef
Wszystko (kod, decyzje, pytania) żyje w jednym projekcie. Nie ma drugiego miejsca — jak czegoś nie ma w Linearze, to nie istnieje.

---

## Ustawienie raz (każdy u siebie)

Wejdź w projekt → sortowanie ustaw na **Title ↑**. Tickety ułożą się `01 → 25` w kolejności pracy. Zapisz jako domyślny widok.

Cztery statusy, przez które przechodzi ticket:
`Backlog` (leży) → `Todo` (następne do wzięcia) → `In Progress` (robione teraz) → `Done` (skończone).

**`In Progress` = "to jest moje, robię to teraz".** To Wasz jedyny sygnał "kto nad czym pracuje" — bez pytania na Slacku patrzysz na tablicę.

---

## Programista

**Które tickety, w jakiej kolejności.** Bierzesz od góry: `01, 02, 03…`. Numer w tytule = kolejność. Nie przeskakujesz — każdy `◇ Decision` stoi tuż przed swoim slice'em, bo trzeba go rozstrzygnąć, zanim zaczniesz kodować to, czego dotyczy.

**Start dzisiaj:** `01 · F-01 · App shell` (już w Todo). Potem `02 · F-02`. Dopiero przy `03` pierwszy raz potrzebujesz decyzji.

**Twój codzienny flow:**
1. Bierzesz najwyższy ticket w `Todo`, przypisujesz na siebie, przeciągasz na `In Progress`.
2. Kopiujesz nazwę brancha z ticketu (pole „Copy git branch name"), `git checkout -b <nazwa>`.
3. W tytule commita/PR wpisujesz numer ticketu, np. `POL-5`. Linear sam podłączy PR i przy mergu przerzuci ticket na `Done` — nie musisz klikać.
4. Odhaczasz checklistę „Definition of Done" w ticketcie.

**Gdy trafisz na pytanie biznesowe** (czegoś nie wiesz, bo to nie kod tylko decyzja produktowa/prawna):
- Jeśli to jeden z gotowych `◇ Decision` — on już czeka. Cztery z nich są już przypisane na kolegę (patrz niżej).
- Jeśli to nowe pytanie — twórz ticket, daj etykietę `biznes`, przypisz na kolegę, wpisz pytanie w opisie albo komentarzu. On dostanie powiadomienie.

**Dwa „nie zapomnij" (zignorowanie boli wiele ticketów później):**
- `04 · S-01` — w T&Cs musi wejść klauzula „chats are corporate property". Bez niej `22 · S-10` jest nielegalny.
- `08 · S-03` — telefon pracownika zbierasz tu, ale RLS ma go chować aż do wpisu w `phone_reveal_log` (dopiero `13 · S-06`). Zaprojektuj ten rozdział od razu.

**Punkt kontrolny:** po `13 · S-06` (north star) macie działającą całą hipotezę produktu. Wszystko od `14` w dół tylko dokłada wartość.

---

## Biznes

**Gdzie wejść.** Projekt polyGo MVP (link na górze) → ustaw filtr **Assignee = ja** albo **Label = biznes**. To Twoja lista: „co Maciek ode mnie potrzebuje". Nic poza tym nie musisz oglądać.

**Co tam jest.** Tickety, w których Maciek implementuje coś i utknął na pytaniu, na które tylko Ty znasz odpowiedź (produktowe, prawne, o branży). W każdym jest opisana sytuacja, opcje do wyboru i zwykle rekomendacja.

**Co robisz z ticketem:**
1. Otwierasz, czytasz pytanie i opcje.
2. **Piszesz decyzję w komentarzu** (np. „Wybieram A, bo…"). To ważne — decyzja musi być zapisana przy ticketcie, nie w rozmowie ustnej, inaczej za miesiąc nikt nie pamięta dlaczego tak.
3. Przerzucasz ticket na `Done`.

Tyle. Po tym Maciek jest odblokowany i koduje dalej.

**Czeka na Ciebie teraz (4 rzeczy):**
- `POL-22` — firma edytuje swój NIP: znika z katalogu na czas ponownej weryfikacji, czy zostaje widoczna?
- `POL-23` — co znaczy „ostatnia aktywność" firmy w sortowaniu wyników (ostatnia wiadomość vs ostatnie logowanie)?
- `POL-27` — czy szef widzi czaty zwolnionego pracownika na żywo, czy tylko historię? (kwestia RODO)
- `POL-29` — jak ma wyglądać czat po zablokowaniu firmy dla drugiej strony?

**Włącz powiadomienia** (Settings → Notifications: email albo Slack), inaczej przypisania będą lądować tylko w aplikacji i ich nie zauważysz.

---

## Gdzie sprawdzić „nad czym teraz pracujemy"

- **Co się dzieje w tej chwili:** widok projektu → kolumna/filtr `In Progress`. To pokazuje, co każdy z Was ma aktualnie w rękach.
- **Ogólny postęp:** nagłówek projektu pokazuje pasek „ile z 25 zrobione".
- **Co czeka na decyzję biznesu:** filtr `Label = biznes`.
- **Co jest następne w kolejce:** najwyższy numer w `Todo`.

Zasada na dwie osoby: zanim weźmiesz nowy ticket, zerknij, czy nie jest `In Progress` u drugiego i czy jego blocker (`◇ Decision` nad nim) jest już `Done`. Linear ostrzeże, jak weźmiesz coś zablokowanego.