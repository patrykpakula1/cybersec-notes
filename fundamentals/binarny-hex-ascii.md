# System binarny, hex, ASCII/Unicode

Fundament tego, jak komputer w ogóle reprezentuje dane. Suchy temat, ale wraca wszędzie — w hashach, logach, analizie malware.

## Binarny — podstawa wszystkiego
Komputer zna tylko dwa stany: włączone/wyłączone = 1/0 = **bit**.
Bogactwo informacji nie bierze się z tego, że pojedynczy bit robi coś złożonego — bierze się z KOMBINACJI wielu bitów.

Przykład z kolorami RGB: 3 przełączniki (R, G, B), każdy on/off = 2×2×2 = 8 możliwych kolorów.
- `000` = wszystko wyłączone = czarny
- `111` = wszystko włączone = biały
- `100` = tylko czerwony = czerwony

To ta sama logika co chmod: `rwx` to trzy przełączniki, `111` (binarnie) = `7` = wszystkie włączone.

## Hex — skrót dla binarnego
Binarny jest precyzyjny, ale nieczytelny i łatwo się pomylić (długie ciągi 0 i 1).
**Jedna cyfra hex = dokładnie 4 bity.** 4 bity dają 16 kombinacji (2^4=16), stąd hex ma 16 cyfr: 0-9, potem A-F (bo brakuje symboli na 10-15).

Konwersja: podziel ciąg binarny na grupy po 4 bity (od prawej), każdą zamień na 1 cyfrę hex, sklej wynik.
Przykład: `1010 0011` → `A` `3` → `A3`

Hex jest wszędzie w cyber: kolory (#FF5733), hashe (MD5/SHA wyglądają jak długi hex), adresy MAC, zrzuty pamięci, analiza malware.

## ASCII — jak liczby stają się literami
Komputer nie zna liter, zna tylko liczby. ASCII to tabela: każdej literze przypisana liczba.
- `A` = 65 (hex `41`)
- `a` = 97 (hex `61`)
- Litery są W KOLEJNOŚCI (a=61, b=62, c=63 w hex) — dzięki temu sortowanie alfabetyczne to dla komputera zwykłe sortowanie liczb.
- Ta kolejność to też podstawa szyfru Cezara (przesunięcie liter o stałą liczbę pozycji w tabeli).

Przykład łańcucha: tekst → binarny → hex → odczyt z tabeli ASCII → litera na ekranie.
`54 72 79` w hex = `T r y` w ASCII.
`0a` (hex) = nie litera, tylko znak nowej linii (Enter/`\n`) — nawet niewidoczne znaki mają swój numer.

## Ograniczenie ASCII i polskie znaki
ASCII ma tylko 128 znaków (7 bitów) — starcza na angielski, nie starcza na ł, ń, ą, ę.
Stąd rozszerzone standardy: ISO-8859-1 (Europa Zachodnia: ü, é, ñ), ISO-8859-2 (Europa Środkowa: ł, ń, č — polski tu wchodzi).

WAŻNE: jeśli plik zapisany w jednym standardzie jest odczytany w innym, polskie litery zamieniają się w krzaczki. To dokładnie ten efekt z życia, gdy otwierasz plik i zamiast "ł" widać dziwny znak — to nie awaria, to niedopasowanie kodowania.

## Unicode i UTF-8/UTF-16
ASCII i ISO-8859 nie starczają na WSZYSTKIE języki świata (japoński, chiński, emoji itd.) — stąd Unicode, uniwersalna tabela obejmująca praktycznie wszystkie znaki.
- **UTF-8** — zmienna długość zapisu (znaki angielskie krótkie, inne dłuższe)
- **UTF-16** — zwykle stała długość 2 bajtów dla większości znaków

Pułapka z praktyki: podobne wizualnie znaki (np. dwie różne katakany シ i ツ) mogą się różnić subtelnie, a dać zupełnie inny wynik kodowania. Trzeba wklejać dokładnie ten znak, o który pytanie, nie wizualnie podobny.

## Po co to w SOC (żeby nie było tylko teorią)
- Analityk widzi w logu/dumpie pamięci ciąg wyglądający jak bezsensowne litery i cyfry → to prawdopodobnie hex, konwerter zamienia go na czytelny tekst
- Hashe (odciski plików/haseł) zapisane są w hex
- Analiza malware często wymaga czytania surowych bajtów w hex i rozpoznawania w nich tekstu/struktur
- Nie trzeba konwertować w głowie — trzeba wiedzieć, że to istnieje i sięgnąć po narzędzie (konwerter), gdy sytuacja tego wymaga

## Szczera uwaga
Ten temat nie wciąga tak jak Linux czy ataki — i to normalne, nie każdy temat musi. Wystarczy znać sedno (co to jest i po co), a szczegółowe konwersje robić narzędziem, nie z głowy.
