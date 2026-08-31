# Chmura (Cloud Computing)

**Chmura = wynajmujesz cudze serwery przez internet, na żądanie, zamiast kupować i trzymać własne.** Płacisz za to, czego używasz, skalujesz w minuty, nie martwisz się sprzętem.
Analogia: kiedyś każdy miał własny generator prądu (fizyczne serwery). Chmura to podłączenie do sieci elektrycznej — bierzesz prąd ile trzeba, płacisz za zużycie.

## Ewolucja do chmury (skąd się wzięła)
Chmura nie pojawiła się nagle — to efekt lat zmian w tym, jak używano serwerów:
1. **Fizyczne serwery** (lata 60 – 2000) — własne serwery w budynku firmy. Jeden serwer = jedno zadanie. Drogie, wolno się skalowało, często stały niewykorzystane.
2. **Wirtualizacja** (1999–2006) — wiele maszyn wirtualnych na jednej fizycznej. Lepsze wykorzystanie sprzętu. (To już znam — hypervisor, VM.)
3. **Automatyzacja i zdalne zarządzanie** (2003–2006) — serwery zarządzane przez internet, pierwsza automatyzacja, mniej ręcznej roboty.
4. **Cloud / start AWS** (2006) — przełom: wynajmujesz wirtualne komputery na żądanie, elastyczne skalowanie w minuty, zero posiadania sprzętu.
5. **Modern Cloud** (2012–dziś) — AWS, Azure, Google Cloud. Kontenery (Docker). Skupienie na aplikacjach, nie serwerach. Skala globalna.

Każdy etap rozwiązywał problem poprzedniego.

## Typy chmury (KTO ma serwery)
- **Public (publiczna)** — serwery dostawcy, współdzielone z innymi firmami. Tanie, łatwo skalować, zero zarządzania sprzętem. Dla startupów, stron, aplikacji. → mieszkanie w bloku (tanio, ktoś inny dba o budynek)
- **Private (prywatna)** — chmura tylko dla jednej firmy. Większa kontrola, bezpieczeństwo, zgodność z przepisami. Dla banków, szpitali, rządu (dane wrażliwe). → własny dom (drożej, ale w pełni Twój)
- **Hybrid (hybrydowa)** — miks obu. Wrażliwe dane trzymasz prywatnie, a przy dużym ruchu skalujesz publicznie. Dla e-commerce (np. sklep w Black Friday). → dom + wynajem magazynu na święta

## Modele usług — IaaS / PaaS / SaaS (ILE sam ogarniam)
Kluczowa zasada: **im dalej od IaaS do SaaS, tym więcej ogarnia dostawca, a mniej ja.**

- **IaaS (Infrastructure as a Service)** — wynajmuję surową infrastrukturę (serwery, dysk, sieć). Dostawca ogarnia fizyczny sprzęt, ale JA zarządzam systemem i aplikacją. Najwięcej kontroli, najwięcej mojej roboty. → puste mieszkanie / kupuję składniki i piekę pizzę sam
- **PaaS (Platform as a Service)** — dostawca ogarnia infrastrukturę I system. Ja tylko buduję i wgrywam aplikację, nie martwię się serwerami. → umeblowane mieszkanie / gotowe ciasto, tylko składam
- **SaaS (Software as a Service)** — dostawca ogarnia WSZYSTKO. Ja tylko używam gotowej aplikacji przez przeglądarkę. Zero zarządzania. → hotel / pizza na telefon. Np. Gmail, Zoom, Netflix.

TEST na rozróżnienie: "Czy sam instaluję / zarządzam systemem operacyjnym?"
- TAK → **IaaS** (moja Ubuntu w VirtualBox = IaaS, bo sam stawiałem system!)
- NIE, dostaję gotowy system, wgrywam tylko apkę → **PaaS**
- Nie mam nawet dostępu do systemu, tylko klikam gotowe → **SaaS**

MOJA ZASADA: **"punkt widzenia zależy od punktu siedzenia"** — ten sam produkt jest różnym modelem zależnie od tego, kim jestem w łańcuchu. Netflix dla widza = SaaS (wchodzę na gotowe), ale Netflix jako firma używa IaaS od AWS (wynajmuje surowe serwery i buduje na nich). To decyduje, za jakie bezpieczeństwo się odpowiada (shared responsibility).

## EC2 (przykład IaaS w praktyce)
Amazonowy (AWS) wirtualny komputer w chmurze. Jak VM, tylko stoi na serwerach Amazona, nie u mnie. Tworzę, używam, zmieniam rozmiar wg potrzeb.
- **Instance Type** (t3.micro, m5.large...) = jak mocny komputer. Większy = więcej CPU/RAM = mocniejszy, ale droższy. Dobiera się do potrzeb.
- Cyber często wymaga IaaS/EC2, bo trzeba pełnego dostępu do systemu (instalować narzędzia, symulować ataki i obronę).

## Koszty (WAŻNE — praktyka z labu)
- **Płacę TYLKO za DZIAŁAJĄCE maszyny** (status running = kasa, stopped = 0, ale dane zostają)
- Mocniejsze dużo droższe: w labie t3.micro = 10 credits, m5.large = 70 (7x więcej!)
- Wyłączanie nieużywanych = oszczędność: w labie ze 170 na 30 credits/month po zatrzymaniu 2 drogich maszyn
- Przewaga chmury nad fizycznym serwerem: fizyczny płacisz zawsze (kupiony), chmurę wyłączasz = przestajesz płacić

## Korzyści chmury
skalowalność, self-service na żądanie, płacisz tylko za użycie, bezpieczeństwo (dostawca chroni infrastrukturę), wysoka dostępność (działa mimo awarii części), globalny dostęp.

## Główni dostawcy
- **AWS** (Amazon) — lider, największy, najwięcej usług
- **Azure** (Microsoft) — mocny w firmach/enterprise
- **Google Cloud (GCP)** — dobry w danych, AI, ML
Plus: Alibaba (Azja), IBM, Oracle.

## Jak firmy używają chmury
Netflix (cały na AWS, skaluje globalnie), Spotify, Instagram, sklepy online (łapią skok ruchu w Black Friday bez kupowania stałego sprzętu). Powód: skupiają się na produkcie zamiast babrać w zarządzaniu sprzętem.

## W cyber / SOC
- **Shared responsibility (współdzielona odpowiedzialność)** — kto za co odpowiada w bezpieczeństwie zależy od modelu. W IaaS JA zabezpieczam system + aplikację (dostawca tylko sprzęt). W SaaS prawie wszystko dostawca. Firmy myślą "jest w chmurze = bezpieczne" i zapominają o swojej działce = dziura.
- **Nagle działająca maszyna, której nikt nie zamawiał = czerwona flaga** 🚩 — możliwy atak, np. ktoś odpalił kryptokoparki na cudzy koszt (realny, popularny atak — złodziej pali czyjąś kasę w chmurze).
