# iptables — podstawy blokowania ruchu

## Zadanie
Odrzucić cały ruch przychodzący z adresu 32.122.195.63.

## Komenda 
```
iptables -A INPUT -s 32.122.195.63 -j DROP
```

## Rozbicie na klocki
- `iptables` — nazwa zapory sieciowej w Linuksie
- `-A INPUT` — dodaj regułę do ruchu **przychodzącego** (INPUT = to, co przychodzi do mnie)
- `-s 32.122.195.63` — **source**, czyli źródło; z którego adresu
- `-j DROP` — akcja: odrzuć pakiet (po cichu wywal)

## Co zapamiętać
Schemat `-A INPUT -s [adres] -j DROP` to podstawa blokowania złych adresów w blue teamie.
Adres wpisuję BEZ kropki na końcu.
