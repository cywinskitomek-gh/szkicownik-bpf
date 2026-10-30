# Szkicownik nut

Piano roll do rysowania melodii palcem lub rysikiem (iPhone, iPad, Mac) i przenoszenia jej do OpenMusic
jako chord-seq (pudełko `chseq-from-text` z biblioteki My_functions) albo do Cubasis/Cubase jako plik MIDI.

Adres: https://cywinskitomek-gh.github.io/szkicownik-bpf/nuty/
Instalacja na iPhonie: Safari → Udostępnij → „Do ekranu początkowego”; raz otwórz z internetem, potem działa też bez sieci.

## Obsługa

- **Jeden palec** rysuje nuty po siatce kwantyzacji (melodia jednogłosowa – nowa nuta zastępuje starą w tym samym miejscu).
- **Dwa palce**: rozsuwanie w poziomie powiększa czas, w pionie – wysokość wierszy; przesuwanie przewija.
- **Klawiatura z lewej**: przeciągnięcie przewija oktawy. **Linijka taktów u góry**: przeciągnięcie przewija takty.
- Na Macu: kółko/gładzik przewija (Shift – w poziomie), Ctrl + kółko (szczypanie na gładziku) powiększa.
- Okienko nad palcem pokazuje dźwięk (C3 = 6000 midicentów) i pozycję takt.miara.krok.
- **Gumka** usuwa nuty, **Cofnij** cofa ostatnie pociągnięcie, **Odtwórz** gra prostym dźwiękiem, **Pokaż wszystko** dopasowuje widok.
- „Łącz powtórzony dźwięk” – ta sama wysokość w jednym pociągnięciu daje jedną dłuższą nutę; wyłączone – osobne nuty co krok.
- „Odsłuch” – przy rysowaniu słychać rysowaną nutę, a przytrzymanie klawisza po lewej gra jego dźwięk (klawisz podświetla się na czerwono). Bezpiecznik: gdy palec stoi w miejscu dłużej niż 2 s, dźwięk gaśnie sam. Przeciągnięcie po klawiaturze nadal przewija oktawy.

## Ustawienia

Kwantyzacja (1/4, 1/8, 1/8 triola, 1/16, 1/16 triola, 1/32), tempo, metrum (ćwierćnuty w takcie), liczba taktów, velocity.

## Eksport

- **Kopiuj dla OM** / **Zapisz plik .txt** – tekst dla pudełka `chseq-from-text`:

```
;; nuty-pad: melodia  (tempo 120, metrum 4/4, velocity 100)
(6000 6400 6700)     ; wysokości, midicenty
(0 500 1000)         ; początki, ms
(500 500 1000)       ; długości, ms
```

- **Zapisz plik .mid** – MIDI (typ 0, 480 PPQ, z tempem i metrum) do Cubasis, Cubase albo OM.

## Aktualizacja

Po zmianie plików podnieś w `sw.js` numer wersji (`szkicownik-nut-v2` → `v3`).
