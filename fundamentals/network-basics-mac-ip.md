# Sieci — podstawy: identyfikacja urządzeń, MAC spoofing, ping

## Dwa sposoby identyfikacji urządzenia
Analogia z materiału: urządzenie ma dwie tożsamości, tak jak człowiek ma imię i odciski palców.
- **IP address** = imię — może się zmieniać, przypisywane przez sieć, w której akurat jesteś
- **MAC address** = odcisk palca — w teorii stały, wgrany fabrycznie w kartę sieciową, unikalny

## Adres IP
Zestaw liczb podzielony na cztery oktety. Dwa typy:
- **Prywatny** — identyfikuje urządzenie wewnątrz lokalnej sieci (dom, firma). Wiele urządzeń, różne prywatne adresy.
- **Publiczny** — identyfikuje całą sieć na zewnątrz, w internecie. Wszystkie urządzenia za tym samym routerem wychodzą pod JEDNYM wspólnym publicznym adresem.

Analogia: blok mieszkalny — każde mieszkanie ma numer wewnętrzny (prywatny IP), ale cały budynek ma jeden adres na kopercie z zewnątrz (publiczny IP).

### IPv4 vs IPv6
- IPv4 — ok. 4,29 miliarda adresów (2^32). Za mało na miliardy urządzeń na świecie dziś.
- IPv6 — 340 trylionów+ adresów (2^128). Rozwiązuje problem wyczerpywania się puli.

## Adres MAC (Media Access Control)
Numer seryjny fizycznej karty sieciowej, wgrany przez producenta. Format: 12 znaków hex, w parach oddzielonych dwukropkiem, np. `a4:c3:f0:85:ac:2d`.
- Pierwsze 6 znaków = producent karty sieciowej
- Ostatnie 6 = unikalny numer tej konkretnej sztuki

MAC to jedna cyfra hex = 4 bity (powtórka z poprzedniej notatki o binarnym/hex).

## MAC spoofing — atak, który zrobiłem w praktyce
Mimo że MAC ma być "niezmienny", da się go podrobić programowo w kilka sekund w ustawieniach systemu. Urządzenie podszywa się pod cudzy, zatwierdzony adres MAC.

Scenariusz z labu (hotelowe Wi-Fi): router wpuszcza tylko urządzenia z zatwierdzonym MAC (np. te, które zapłaciły za dostęp). Zmieniając swój MAC na taki jak u zaakceptowanego urządzenia, router zaczyna traktować mnie jak tamto urządzenie i przepuszcza ruch.

DLACZEGO to jest słabość: jeśli firewall/router ufa urządzeniu WYŁĄCZNIE na podstawie adresu MAC, to całe zabezpieczenie stoi na czymś łatwym do podrobienia. Ten sam wzorzec co przy hasłach czy uprawnieniach — pojedyncza, łatwa do obejścia bariera jako jedyna linia obrony to zawsze dziura.

Wniosek dla obrońcy: filtrowanie po samym MAC nigdy nie powinno być JEDYNYM zabezpieczeniem — potrzeba dodatkowych warstw (hasło, certyfikat). Wielowarstwowa obrona, nie pojedynczy zamek.

## Ping i ICMP
**Ping** = podstawowe narzędzie sprawdzania, czy połączenie z urządzeniem istnieje i jak jest szybkie.

Mechanizm: wysyła pakiet **ICMP echo** ("jesteś tam?") do celu. Jeśli cel działa, odsyła **ICMP echo reply** ("tak, jestem"). Ping mierzy czas między wysłaniem a odpowiedzią (w milisekundach).

WAŻNE rozróżnienie: ICMP nie przesyła żadnej użytecznej treści (nie jak TCP/HTTP, które przesyłają dane/strony) — jego jedyne zadanie to sprawdzanie stanu połączenia i diagnostyka.

Składnia: `ping adres_ip_lub_url`
Przykład: `ping 8.8.8.8` (8.8.8.8 = publiczny serwer DNS Google, powszechnie używany do testowania łączności, bo prawie zawsze dostępny)

Jak sprawdzić pełną składnię dowolnej komendy w Linuksie, gdy nie pamiętam opcji: `man nazwa_komendy` (np. `man ping`) — wbudowany podręcznik, zawsze dostępny w terminalu.

## Po co to w SOC
- Adres MAC bywa jedynym zabezpieczeniem w słabo zaprojektowanych sieciach — analityk sprawdza, czy filtrowanie nie opiera się wyłącznie na nim
- Podejrzenie MAC spoofingu: to samo urządzenie fizyczne nagle "zmienia tożsamość" w logach, albo dwa urządzenia w sieci mają identyczny MAC
- Ping to pierwszy, najprostszy krok diagnostyki sieci — sprawdzenie, czy cel w ogóle odpowiada, zanim przejdzie się do głębszej analizy
