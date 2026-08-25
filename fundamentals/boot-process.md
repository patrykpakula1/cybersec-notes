# Proces bootowania (boot process)

Co się dzieje od naciśnięcia power do startu systemu.

## Kolejność
1. **Press Power Button** — naciskam włącznik, prąd idzie do płyty głównej
2. **Firmware Starts** — budzi się firmware (BIOS/UEFI), "program przed systemem" wgrany na stałe w płytę
3. **POST** (Power-On Self-Test) — komputer sprawdza sam siebie: RAM, CPU, dysk, GPU. Jak coś nie gra → piknięcia / błąd
4. **Select Boot Device** — firmware wybiera, SKĄD startować (dysk, USB, płyta, sieć) wg listy priorytetów
5. **Start Bootloader** — mały program, który ładuje właściwy system operacyjny (Windows/Linux)

## Po co to w SOC
Malware w bootloaderze albo firmware ładuje się PRZED systemem i antywirusem → trudny do wykrycia i bardzo groźny.
Znajomość tego łańcucha = wiem, gdzie atak może się ukryć.

## Zapamiętać
Guzik → firmware się budzi → sprawdza sprzęt (POST) → wybiera skąd startować → bootloader ładuje system.
Każdy krok przekazuje pałeczkę następnemu.
