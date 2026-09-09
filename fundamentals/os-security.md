# Bezpieczeństwo systemów operacyjnych

## Warstwy komputera (powtórka)
Hardware (CPU, RAM, dysk) → Operating System → Software (programy, aplikacje)
OS siedzi między sprzętem a aplikacjami i pozwala im korzystać ze sprzętu wg określonych reguł.

## Triada CIA — fundament całego bezpieczeństwa
Każdy atak narusza co najmniej jeden element, każde zabezpieczenie któryś chroni.

- **Confidentiality (poufność)** — tylko uprawnieni mają dostęp do danych. (moje chmod 600 na kluczu SSH = poufność). Chronią ją: uwierzytelnianie, szyfrowanie, uprawnienia.
- **Integrity (integralność)** — nikt nie może ZMIENIĆ danych bez uprawnienia (na dysku ani w trakcie przesyłania). Uprawnienie `w` (write) w rwx = kontrola integralności.
- **Availability (dostępność)** — system i dane działają, kiedy ich potrzebuję. Atak DDoS i ransomware uderzają właśnie w to.

Przykład: ransomware szyfruje pliki → narusza głównie DOSTĘPNOŚĆ (nie mam dostępu do własnych plików), często też poufność (jeśli dane najpierw wykradziono).

## Trzy słabości atakowane przez napastników

### 1. Uwierzytelnianie i słabe hasła
Uwierzytelnianie = weryfikacja tożsamości. Trzy sposoby:
- **Coś, co WIESZ** — hasło, PIN
- **Coś, czym JESTEŚ** — odcisk palca, twarz
- **Coś, co MASZ** — telefon (SMS), token

2FA/MFA = wymóg DWÓCH RÓŻNYCH kategorii naraz (np. hasło + SMS = wiesz + masz). Dwa hasła to NIE 2FA (obie z tej samej kategorii).

Hasła są najsłabsze, bo ludzie używają prostych albo tych samych wszędzie. Atakujący nie zgaduje losowo — leci po liście najpopularniejszych haseł (NCSC publikuje top 100 000).

### 2. Słabe uprawnienia plików — least privilege
**Zasada najmniejszych uprawnień**: każdy dostaje DOKŁADNIE tyle dostępu, ile potrzebuje do pracy — nic więcej. Krótko: "kto ma dostęp do czego?".

To dokładnie to, co robiłem z chmod: klucz 600, notatka 644, skrypt 755 — decydowałem, kto ile może.

Słabe uprawnienia uderzają w DWA elementy triady: poufność (ktoś czyta pliki, których nie powinien) + integralność (ktoś modyfikuje pliki, których nie powinien). Czyli `r` i `w` z rwx = C i I z CIA.

### 3. Złośliwe programy
- **Trojan** — daje atakującemu dostęp do systemu → czyta i modyfikuje pliki (narusza poufność i integralność)
- **Ransomware** — szyfruje pliki, żąda okupu za klucz → narusza dostępność (i często poufność)

## Konta z pełnym dostępem
- **root** — Linux, Android, Apple. Pełny, nieograniczony dostęp.
- **administrator** — Windows. To samo.
Cel atakującego: zdobyć root/administrator = **privilege escalation** (przejście z ograniczonego usera do pełnej kontroli).

## Praktyka — atak na system (byłem po stronie atakującego)
Układ labu: **AttackBox** (maszyna atakująca, czerwona, z narzędziami) atakuje **Lab machine** (cel), w izolowanym środowisku.

WAŻNE: zawsze patrzeć na PROMPT, żeby wiedzieć, gdzie jestem:
- `root@AttackBox` = moja maszyna atakująca
- `johnny@cel` = zalogowany na celu jako johnny

### Krok 1 — zdobycie dostępu (zgadywanie hasła)

Enter → czekać na OSOBNĄ linię `password:` → wpisać hasło (w ciemno, NIC się nie wyświetla) → Enter.
Próbować kolejno haseł z listy popularnych, aż jedno przejdzie.
WAŻNE: nie wpisywać hasła w tej samej linii co komenda ssh — najpierw komenda, potem czekać na pytanie o hasło.

### Krok 2 — eskalacja przez history
Po zalogowaniu jako johnny:\
Wypisuje wszystkie komendy usera. Szukać linii, która NIE jest komendą — przypadkowy ciąg znaków, który user wklepał PRZEZ POMYŁKĘ zamiast polecenia. To bywa hasło roota zostawione w historii.

## Po co to obrońcy (SOC)
- `history` to jedno z pierwszych miejsc, gdzie zagląda i atakujący (szuka zostawionych haseł), i obrońca (bada, co ktoś robił na systemie)
- Zrozumienie ataku (zgadywanie haseł, privilege escalation) jest konieczne, żeby to wykrywać i blokować — nie da się bronić czegoś, czego się nie rozumie od strony ataku
- Słabe hasła, słabe uprawnienia, hasła w historii = realne dziury, które analityk sprawdza

## Pułapki z praktyki
- Wpisanie hasła sklejone z komendą ssh → bash wpada w tryb `>` (czeka na dokończenie). Naprawa: Ctrl+C.
- Przy wpisywaniu hasła w SSH nic się nie wyświetla — to normalne, wpisywać w ciemno.
- `<FILENAME>`, `<IP>` itd. w materiałach to placeholdery — wstawić własną wartość, nie kopiować dosłownie.
- Maszyny THM czasem nie wstają / sesja się rwie — to nie mój błąd, odświeżyć albo poczekać.
