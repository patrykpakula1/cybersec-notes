# Linux — podstawy terminala

## Poruszanie się
- `pwd` — gdzie jestem (pokazuje ścieżkę, np. /home/user)
- `ls` — co tu jest (lista plików i folderów)
- `ls -l` — to samo, ale ze szczegółami (uprawnienia, właściciel, rozmiar, data). Uwaga: małe L, nie jedynka!
- `ls -a` — pokazuje też ukryte pliki (te z kropką na początku, np. .bashrc, .ssh)
- `cd folder` — wejdź do folderu
- `cd ..` — wróć do góry (dwie kropki!)

## Tworzenie
- `touch nazwa.txt` — tworzy pusty plik

## Uprawnienia (WAŻNE w cyber)
Zapis typu `-rw-r--r--` czyta się:
- 1. znak: `-` = plik, `d` = katalog
- potem 3 grupy po 3 znaki: WŁAŚCICIEL | GRUPA | RESZTA ŚWIATA
- `r` = read (czytaj), `w` = write (pisz), `x` = execute (wykonaj), `-` = brak

### chmod — zmiana uprawnień
`chmod 600 plik.txt` → ustawia uprawnienia liczbowo

Liczby: read=4, write=2, execute=1 (sumuje się)
- 6 = rw- (4+2)
- 7 = rwx (4+2+1)
- 4 = r--
- 0 = --- (nic)

Trzy cyfry = właściciel / grupa / reszta:
- `600` = `-rw-------` → tylko właściciel (wrażliwe pliki: klucze, hasła)
- `644` = `-rw-r--r--` → właściciel pisze, reszta czyta (typowy plik)
- `700` = `-rwx------` → właściciel wszystko, reszta nic (prywatny skrypt)
- `755` = `-rwxr-xr-x` → właściciel wszystko, reszta czyta+wykonuje

## Po co to w SOC
Źle ustawione uprawnienia = dziura bezpieczeństwa. Plik z hasłami dostępny dla wszystkich (644 albo gorzej) to czerwona flaga. Klucz SSH bez 600 → SSH się nie uruchomi. Analityk ciągle patrzy, czy coś nie jest zbyt otwarte.

## Uwagi z praktyki
- Linux rozróżnia wielkość liter: `cd` działa, `cD` nie
- Nazwy muszą się zgadzać co do litery: `Downloads` (z s), nie `Download`
- `-l` (litera L) to szczegóły, `-1` (jedynka) to co innego — łatwo pomylić
