# Uprawnienia w Linuksie (chmod)

## Jak czytać zapis typu -rw-r--r--

Dzielisz na 4 części:
 rw-      r--      r--
 - 1. znak: `-` = plik, `d` = katalog
- potem 3 paczki po 3 znaki: WŁAŚCICIEL | GRUPA | RESZTA ŚWIATA

## Trzy okienka w każdej paczce (zawsze w tej kolejności: r-w-x)
- `r` = read → czy mogę **czytać**
- `w` = write → czy mogę **pisać** (zmieniać)
- `x` = execute → czy mogę **uruchomić**
- litera = TAK, mogę | myślnik `-` = NIE, nie mogę

Liczy się POZYCJA, nie ilość liter:
- `r--` = tylko czyta
- `-w-` = tylko pisze
- `--x` = tylko uruchamia

## Zapis liczbowy (chmod)
Każda litera ma wartość, sumujesz je:
- `r = 4`
- `w = 2`
- `x = 1`

Przykłady (jedna paczka):
- `rwx` = 4+2+1 = **7** (wszystko)
- `rw-` = 4+2 = **6** (czyta+pisze)
- `r-x` = 4+1 = **5** (czyta+uruchamia)
- `r--` = **4** (tylko czyta)
- `---` = **0** (nic)

Trzy cyfry = trzy paczki (właściciel / grupa / reszta):
- `chmod 600` = `-rw-------` → tylko właściciel (wrażliwe pliki: klucze, hasła)
- `chmod 644` = `-rw-r--r--` → właściciel pisze, reszta czyta (typowy plik)
- `chmod 755` = `-rwxr-xr-x` → właściciel wszystko, reszta czyta+uruchamia (programy, foldery)

## WAŻNE: 5 vs 6 — plik czy program?
- **6 = rw-** (czyta+pisze, NIE uruchamia) → zwykły **plik z danymi** (tekst, log, config, zdjęcie). Nie ma x, bo nie ma czego uruchamiać.
- **5 = r-x** (czyta+uruchamia, NIE pisze) → **program / skrypt / folder**. Ma x, bo się to wykonuje. Brak w, żeby nikt nie podmienił zawartości.

Reguła kciuka:
- widzę `x` → to program, skrypt albo folder
- brak `x`, tylko `rw` → zwykły plik z danymi

## Czerwona flaga w SOC 🚩
Jak analityk widzi **plik z danymi (.txt, .log), który ma `x`** (możliwość uruchomienia) — to podejrzane.
Może znaczyć, że ktoś podrzucił złośliwy skrypt udający niewinny plik, albo nadał plikowi możliwość wykonania, żeby odpalić go jako malware.
Pytanie, które zadaje dobry analityk: "Czemu ten zwykły plik tekstowy jest wykonywalny?"

## Sprawdzanie vs zmiana
- `ls -l plik` → tylko PATRZYSZ na uprawnienia (diagnoza)
- `chmod XXX plik` → ZMIENIASZ uprawnienia (naprawa)
Najpierw sprawdź (ls -l), potem napraw (chmod).
