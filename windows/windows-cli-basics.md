# Windows CLI — podstawy Command Prompt

Terminal Windows (CMD). W SOC spotyka się Windows częściej niż Linux (większość komputerów pracowników), więc trzeba znać oba. Ten sam workflow co w Linuksie, inne nazwy komend.

Dlaczego CLI zamiast klikania (wg THM):
- szybsze niż klikanie
- daje więcej kontroli
- wiele narzędzi bezpieczeństwa działa TYLKO w terminalu

## Nawigacja
- `cd folder` — wejdź do folderu (identycznie jak w Linuksie)
- `cd ..` — poziom wyżej
- `cd` — samo, bez argumentu = pokazuje bieżącą ścieżkę (odpowiednik linuksowego `pwd`)
- `dir` — pokaż zawartość folderu (odpowiednik `ls`)
- `dir /a` — pokaż też ukryte pliki (odpowiednik `ls -a`)

Ścieżki w Windows: **backslash `\`** i litery dysków — `C:\Users\Administrator\Documents`
(w Linuksie: ukośnik `/` i `/home/user`)

## Szukanie plików
dir /s nazwa_pliku.txt

Flaga `/s` = przeszukaj WSZYSTKIE podfoldery od bieżącego katalogu i pokaż pełną ścieżkę.
To odpowiednik linuksowego `find . -name plik`.

## Czytanie plików
type plik.txt

Wypisuje zawartość pliku na ekran. Odpowiednik `cat`.

## Standardowy łańcuch pracy (identyczny jak w Linuksie)
`dir /s` (znajdź) → `cd` (idź tam) → `dir` (potwierdź) → `type` (przeczytaj)

## Recon — pytania, które zadaje się systemowi na start
Analityk przed naprawą problemu albo przy badaniu incydentu pyta: kim jestem, co to za maszyna, jaki system, jak podłączona do sieci.

- `whoami` — jako kto jestem zalogowany.
  UWAGA: w Windows zwraca `nazwa-komputera\użytkownik` (host + user), bo Windows myśli w kategoriach domen. W Linuksie zwracało samo `ubuntu`.
- `hostname` — nazwa komputera (identycznie jak w Linuksie)
- `systeminfo` — wersja i szczegóły systemu. Wypluwa DUŻO linii, szukać:
  - `Host Name` — nazwa
  - `OS Name` — np. Microsoft Windows Server 2019 Datacenter
  - `OS Version` — numer wersji/builda
  - `System Type` — 32-bit czy 64-bit
  - lista hotfixów (zainstalowanych poprawek)
- `ver` — sama wersja Windowsa (krócej niż systeminfo)
- `ipconfig` — konfiguracja sieciowa. Szukać:
  - `IPv4 Address` — adres tej maszyny w sieci
  - `Default Gateway` — brama domyślna, przez którą maszyna wychodzi na zewnątrz
  - `Subnet Mask` — zasięg lokalnej sieci

## Windows vs Linux — tabela tłumaczeń
| Zadanie | Linux | Windows |
|---|---|---|
| kim jestem | `whoami` | `whoami` (to samo) |
| nazwa maszyny | `hostname` | `hostname` (to samo) |
| gdzie jestem | `pwd` | `cd` (samo) |
| lista plików | `ls` | `dir` |
| ukryte pliki | `ls -a` | `dir /a` |
| wejdź do folderu | `cd` | `cd` (to samo) |
| znajdź plik | `find . -name X` | `dir /s X` |
| przeczytaj plik | `cat` | `type` |
| wersja systemu | `uname -r`, `cat /etc/os-release` | `systeminfo`, `ver` |
| sieć / IP | `ip a`, `ifconfig` | `ipconfig` |
| separator ścieżki | `/` | `\` |
| katalog domowy | `/home/user` | `C:\Users\user` |
| konto admina | root | Administrator |

## Po co to w SOC
- **systeminfo pokazuje zainstalowane poprawki (hotfixy)** — atakujący sprawdza, czego brakuje, żeby dopasować exploit. Obrońca sprawdza to samo, żeby wiedzieć, czy system jest załatany.
- **ipconfig to mapa sytuacyjna**: IPv4 mówi, którą maszyną jestem w logach; Default Gateway to punkt, gdzie ruch wychodzi na zewnątrz (miejsce na filtrowanie/monitoring — egress); Subnet pokazuje zasięg lokalnej sieci, czyli gdzie atakujący może się przemieszczać "bokiem" (lateral movement).
- Te komendy to pierwsze, co uruchamia analityk albo IT na nieznanej maszynie Windows.

## Pułapki z praktyki
- `<path_to_the file>` w materiałach THM to PLACEHOLDER — nie wpisuje się ostrych nawiasów, tylko własną ścieżkę
- `cd` wchodzi do FOLDERU, nie do pliku — ścieżka kończy się na nazwie katalogu, bez pliku na końcu
- TAB działa też w Windows CLI (autouzupełnianie ścieżek) — warto używać przy długich ścieżkach
- Uwaga na literówki w nazwach folderów (np. `exports_imv` vs `export_imv`) — przepisuj dokładnie albo używaj TAB
