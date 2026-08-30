# Wirtualizacja — hypervisor, VM, kontenery

Teoria tego, co zrobiłem w praktyce, stawiając Ubuntu w VirtualBox.

## Po co wirtualizacja
Dzielisz JEDEN fizyczny komputer na wiele "udawanych" komputerów działających obok siebie. Każdy myśli, że jest osobną maszyną. Analogia: jeden budynek podzielony na mieszkania.

## Hypervisor — "zarządca budynku"
Oprogramowanie, które tworzy i zarządza maszynami wirtualnymi:
- dzieli fizyczny komputer na wiele wirtualnych
- przydziela każdej VM kawałek CPU, RAM, dysku
- trzyma wszystko odizolowane i bezpieczne
- zarządza VM: start, stop, pauza, klonowanie, usuwanie

(VirtualBox = hypervisor.)

### Dwa typy
- **Type 1** — działa BEZPOŚREDNIO na sprzęcie. Szybki. Do serwerów, data center. (VMware ESXi, Hyper-V)
- **Type 2** — działa WEWNĄTRZ systemu (np. na moim Windowsie). Łatwy. Do nauki, testów. (VirtualBox, VMware Workstation)

Prosto: Type 1 = na goły sprzęt (firmy), Type 2 = na system, który już masz (nauka).

Który do czego:
- Type 1: serwer produkcyjny, baza danych, data center
- Type 2: testowanie malware, testy oprogramowania, Kali Linux, nauka

## VM (maszyna wirtualna) — "mieszkanie"
Wirtualny komputer stworzony przez hypervisor. Mimo że wirtualny, działa jak prawdziwy:
- ma własny wirtualny CPU, RAM, dysk, sieć
- może uruchomić dowolny system (Windows, Linux, macOS)
- jest CAŁKOWICIE odizolowany od innych VM — jak jedna padnie, reszta działa

Dlatego moja Ubuntu w VirtualBox nie zepsuje Windowsa — siedzi w izolowanym "mieszkaniu".

## Kontener (container) — lżejsza alternatywa
Małe, izolowane "pudełko" dla JEDNEJ aplikacji, które WSPÓŁDZIELI system z hostem. Lżejsze od VM.
- **Container Image** = gotowy szablon/przepis, z którego tworzy się kontenery (jak forma do odlewu)
- Popularne narzędzie: **Docker**

### VM vs Kontener
- **VM** = pełny komputer z WŁASNYM systemem → ciężki, do poważnych/oddzielnych rzeczy
- **Kontener** = izolowana aplikacja BEZ własnego systemu → lekki, do wielu małych aplikacji obok siebie
- Analogia: VM = osobny dom, kontener = mieszkanie w bloku
- Firma chce hostować wiele małych aplikacji na jednej maszynie → używa KONTENERÓW (VM byłyby za ciężkie)

## Porty sieciowe
Numerowane punkty wejścia, przez które aplikacje gadają przez sieć: 22=SSH, 80=HTTP, 443=HTTPS. (Te same, które blokuję w iptables przez --dport.)

## Dlaczego to KLUCZOWE w cyber
Testowanie malware:
- podejrzany plik odpalasz w VM, nie na prawdziwym kompie
- zainfekuje
