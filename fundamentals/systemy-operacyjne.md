# Systemy operacyjne (OS)

OS = rdzenne oprogramowanie, które koordynuje wszystko na komputerze. Siedzi między userem, aplikacjami a sprzętem — niewidzialny zarządca.

Warstwy:
User → Applications → Operating System → Hardware

Analogia lotniskowa:
- Hardware (CPU, RAM, dysk) = pasy, samoloty, radary
- Applications = linie lotnicze i pasażerowie
- OS = kontrola ruchu lotniczego (kieruje wszystkim, przydziela zasoby, rozwiązuje konflikty)

Bez OS każda aplikacja walczyłaby o sprzęt = chaos. OS to centralny organizator.

## Kernel space vs User space (WAŻNE dla cyber)
- **Kernel space** — strefa uprzywilejowana. Działa tu kernel (serce systemu), ma NIEOGRANICZONY dostęp do sprzętu. = wieża kontroli
- **User space** — strefa ograniczona. Działają tu zwykłe aplikacje, BEZ bezpośredniego dostępu do sprzętu. = linie lotnicze na ziemi

Podział chroni system: jedna zepsuta aplikacja nie wywali całości.

## System call (wywołanie systemowe)
Aplikacja z user space nie dotyka sprzętu sama — musi POPROSIĆ kernel przez system call.
= linia lotnicza radiuje prośbę do wieży, wieża obsługuje bezpiecznie.

## Privilege escalation (eskalacja uprawnień) 🚩
Atak: przeskoczyć z user space do kernel space. Jak malware wejdzie do kernela = nieograniczony dostęp do wszystkiego. Jeden z najgroźniejszych ataków. = włamanie z parteru do wieży kontroli.

## Obowiązki OS
- **Process Management** — tworzy/planuje/kończy programy, dzieli czas CPU
- **Memory Management** — przydziela RAM, IZOLUJE aplikacje od siebie, pamięć wirtualna gdy brak RAM
- **File System Management** — pliki, foldery, ścieżki, uprawnienia (chmod!)
- **User Management** — konta, logowanie (autentykacja), uprawnienia (kto ma dostęp)
- **Device Management** — ładuje sterowniki, uniwersalny sposób gadania ze sprzętem

## GUI vs CLI
- **GUI** — interfejs graficzny, klikanie, ikony. Łatwe, wolniejsze. (mapa: kliknij miejsce)
- **CLI** — komendy tekstowe (ls, cd, chmod). Precyzyjne, szybkie, wymaga wiedzy. (mapa: wpisz współrzędne GPS)
- W cyber RZĄDZI CLI: szybkie, automatyzowalne, a serwery często nie mają GUI.

## OS jako fundament bezpieczeństwa
Zanim wejdzie antywirus, OS już chroni (4 filary, wszystkie znam z Linuksa):
- Authentication — kim jesteś (hasło)
- Permissions — co możesz (rwx/chmod)
- Isolation — proces w swoim pudełku (kernel/user separation)
- System Protection — ochrona krytycznych plików systemu
