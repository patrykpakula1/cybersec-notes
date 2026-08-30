# HTTP i HTTPS — podstawy

## Co to HTTP(S)
- **HTTP** (Hypertext Transfer Protocol) — protokół, którym przeglądarka (client) rozmawia z serwerem, żeby pobrać stronę WWW.
- **HTTPS** — to samo, ale **szyfrowane**. Litera S = Secure. Nikt po drodze nie podejrzy, co przesyłasz (hasła, dane). Dziś standard.
- HTTP jest **bezstanowy (stateless)** — serwer traktuje każde żądanie osobno i NIE pamięta poprzednich. To jak rozmowa z kimś, kto po każdym zdaniu zapomina, o czym była mowa.

## Skoro bezstanowy, to jak strony mnie "pamiętają"?
Przez dodatkowy mechanizm nałożony na HTTP:
- Po zalogowaniu serwer tworzy **identyfikator sesji (session ID)** — zapisany w **cookie** albo tokenie.
- Ten identyfikator leci z każdym kolejnym żądaniem → serwer rozpoznaje, że to Ty, i nie musisz logować się co chwilę.
- **WAŻNE w cyber:** jeśli atakujący ukradnie Twoje cookie/session ID, może **podszyć się pod Ciebie zalogowanego** bez znajomości hasła. Dlatego kradzież sesji to realny atak.

## Metody HTTP (co chcę zrobić z zasobem)
Metoda mówi serwerowi, jaką akcję chcę wykonać. Najważniejsze:
- **GET** — POBIERZ zasób (np. wyświetl stronę). Najczęstsza. Nic nie zmienia, tylko czyta.
- **POST** — WYŚLIJ dane do serwera (np. formularz, logowanie, komentarz). Coś tworzy/zmienia.
- **PUT** — wyślij zasób, zastępując istniejący
- **DELETE** — usuń zasób
- (PATCH, HEAD, OPTIONS, CONNECT, TRACE — rzadsze, na razie nieistotne)

Zapamiętać: GET = biorę, POST = daję.

## Jak działa GET (przepływ)
1. Client (przeglądarka) wysyła żądanie: `GET /index.html`
2. Server odpowiada: kod statusu + zawartość (`200 OK` + strona)
Czyli: klient prosi o stronę, serwer ją odsyła.

## Co to status code (kod statusu) — WAŻNE
Kiedy serwer odpowiada na żądanie, zawsze dołącza **trzycyfrowy kod**, który mówi, JAK poszło. To jak zwrotka: "udało się" / "nie ma tego" / "błąd". Analityk czyta te kody, żeby wiedzieć, co się dzieje w ruchu.

Kody są w grupach wg pierwszej cyfry:
- **1xx** — informacyjne (rzadkie, "trwa przetwarzanie")
- **2xx — SUKCES.** Np. `200 OK` = żądanie się powiodło, masz zasób.
- **3xx — PRZEKIEROWANIE.** Zasób jest gdzie indziej, przeglądarka idzie dalej. Np. `301` = przeniesiono na stałe.
- **4xx — BŁĄD KLIENTA.** To TY (client) coś źle zrobił. Np. `404` = nie znaleziono strony, `403` = zabroniony dostęp, `401` = wymagane logowanie.
- **5xx — BŁĄD SERWERA.** Serwer się wywalił, nie Twoja wina. Np. `500` = wewnętrzny błąd serwera.

Reguła kciuka: **2 = git, 3 = gdzie indziej, 4 = Twój błąd, 5 = błąd serwera.**

## Co widać w DevTools (F12 → zakładka Network)
DevTools to narzędzia deweloperskie w przeglądarce (F12). Zakładka **Network** pokazuje KAŻDE żądanie, jakie strona wysyła — na żywo. Dla każdego widać:
- **Method** — GET/POST itd. (co robił)
- **Status** — kod odpowiedzi (200, 404...)
- **Domain / File** — z jakiego serwera i jaki plik
- **Type** — rodzaj: html, css, js, img

Po kliknięciu w konkretne żądanie dostajesz szczegóły:
- **Scheme** — protokół: HTTP czy HTTPS
- **Host** — nazwa hosta (np. httpdemo.local:8080)
- **Address** — adres IP serwera (np. 127.0.0.1 = "localhost", ten sam komputer)
- **Response** — odpowiedź serwera: nagłówki + treść (np. kod HTML strony)

Odpowiedź dzieli się na dwie części:
- **Response header** — metadane (typ treści, długość, data, jaki serwer)
- **Response body** — właściwa zawartość (np. HTML strony)

## Dlaczego to ważne w SOC
DevTools → Network to okno na ruch HTTP. Analityk patrzy:
- jakie żądania lecą i dokąd (czy nie do podejrzanej domeny)
- jakie metody (nagły POST tam, gdzie nie powinno = ktoś wysyła dane?)
- jakie kody statusu (dużo 404 = ktoś skanuje/szuka ukrytych stron? dużo 401/403 = ktoś próbuje się dostać, gdzie nie wolno?)
To podstawa analizy ruchu webowego — a przy tle web-dev czytam to szybciej niż większość.
