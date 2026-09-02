# Windows — podstawy

Windows to najpopularniejszy OS na komputerach firmowych. W SOC spotyka się go najczęściej, bo to większość maszyn pracowników — trzeba znać jego interfejs i narzędzia bezpieczeństwa.

## Interfejs — podstawy
- **Desktop (pulpit)** — główny obszar roboczy, gdzie żyją pliki, foldery, skróty
- **Taskbar (pasek zadań)** — pasek dający dostęp do aplikacji, narzędzi, ustawień i powiadomień
- **Start Menu (menu Start)** — główny sposób dostępu do aplikacji, ustawień i opcji zasilania (logo Windows)
- **Search (wyszukiwarka)** — szybkie znajdowanie aplikacji, ustawień, plików po wpisaniu frazy
- **File Explorer (eksplorator plików)** — wbudowane narzędzie do przeglądania i organizowania plików i folderów

## Zarządzanie systemem
- **Windows Update** — wbudowane narzędzie aktualizacji: trzyma system, apki i zabezpieczenia aktualne (WAŻNE: nieaktualny system = dziury, które atakujący wykorzystują)
- **Microsoft Store** — natywna aplikacja do instalowania zaufanych programów
- **Windows Settings (ustawienia)** — centralne miejsce konfiguracji systemu, urządzeń, personalizacji, bezpieczeństwa
- **Control Panel (panel sterowania)** — starszy (legacy) interfejs zarządzania, dostęp do konfiguracji systemu

## Narzędzia ważne dla cyber / SOC
- **Task Manager (menedżer zadań)** — monitoruje, co dzieje się w systemie w czasie rzeczywistym (procesy, zużycie zasobów). Analityk szuka tu podejrzanych procesów.
- **Windows Security** — centralny panel wbudowanych narzędzi bezpieczeństwa Windows
- **Windows Defender Firewall** — firewall chroniący przed nieautoryzowanym ruchem sieciowym (odpowiednik iptables z Linuksa — kontroluje, co wchodzi/wychodzi)
- **Windows Defender (antywirus)** — skanuje i wykrywa zagrożenia. Wykrycia widać w "Protection history" → szczegóły pokazują "Affected items" (jakie pliki/klucze rejestru/zadania zostały zainfekowane)

## Co zapamiętać z praktyki (EICAR)
Skanując Defenderem wykrywa się zagrożenia. W szczegółach wykrycia (Affected items) widać CAŁĄ mapę infekcji — nie tylko plik, ale też:
- plik (np. tryhatmemaldoc.txt)
- task scheduler (zadanie harmonogramu — żeby malware uruchamiał się automatycznie)
- rejestr / regkey (żeby przetrwać restart i startować z systemem)
To pokazuje, jak prawdziwy malware się zagnieżdża: nie tylko podrzuca plik, ale wpina się w system, żeby przetrwać. Analityk czyta to jak mapę: gdzie wszędzie się rozlazło.

## Windows vs Linux (szybkie porównanie)
Robią to samo, inaczej nazywają:
- Terminal: bash (Linux) → CMD / PowerShell (Windows)
- ls → dir
- /home/user → C:\Users\user
- root/admin → Administrator
- chmod/rwx → uprawnienia NTFS
- iptables → Windows Defender Firewall
Fundament ten sam, inny dialekt.
