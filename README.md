# Szkicownik BPF

Rysowanie krzywych palcem lub rysikiem (iPhone, iPad, Mac) i przenoszenie ich do OpenMusic jako BPF.
Autor: Tomasz Cywiński. Wczytywanie w OM: pudełko `bpf-from-text` z biblioteki My_functions.

Adres: https://cywinskitomek-gh.github.io/szkicownik-bpf/

W repozytorium są dwa narzędzia:

- **Szkicownik BPF** – krzywe do OpenMusic (opis poniżej), adres jak wyżej.
- **Szkicownik nut** – piano roll do rysowania melodii, eksport do OM (chord-seq) i MIDI:
  https://cywinskitomek-gh.github.io/szkicownik-bpf/nuty/ – [opis i obsługa](#szkicownik-nut).

## Instalacja na iPhonie (działa bez internetu)

1. Otwórz adres w Safari (z internetem).
2. Udostępnij → „Do ekranu początkowego” → Dodaj.
3. Otwórz szkicownik raz z ikony, mając internet. Od tej chwili działa też w trybie samolotowym.

## Rysowanie

- Rysuj od lewej do prawej. Fragment poprawiasz, rysując go jeszcze raz.
- Okienko tuż nad palcem/kursorem pokazuje na żywo współrzędne punktu (przy górnej krawędzi – z lewej strony palca, a w lewym górnym rogu – pod palcem).
- Pierwsza krzywa po otwarciu to przykład (napis „przykład”) – znika przy pierwszym dotknięciu.
- Ostatnia krzywa zostaje zapamiętana w przeglądarce i wraca po ponownym otwarciu.

## Ustawienia

| Pole | Znaczenie |
|---|---|
| Nazwa | nazwa krzywej, trafia do nagłówka i nazwy pliku |
| Zakres y | gotowe zakresy: midicenty 2100–10800, tension 113–244, 0…1, −1…1, sigma 0–2400, albo własny |
| y min, y max | dolna i górna granica y (wpisanie wartości przełącza na „własny”) |
| Oś x | „numer punktu 0…N−1” – x to kolejne liczby całkowite; „własny zakres” – x min i x max wpisujesz sam |
| Punkty | liczba punktów krzywej (2–2000); zmiana przelicza narysowaną krzywą |
| Precyzja | liczba miejsc po przecinku dla y; wartości ujemne zaokrąglają do 10 (−1), 100 (−2, półtony w midicentach), 1000 (−3) |
| Wygładzenie | 0 = bez wygładzania; im więcej, tym łagodniejsza krzywa |

Precyzja ujemna jest ograniczona zakresem y: krok zaokrąglenia nie może przekroczyć 1/4 zakresu
(np. przy 0–100 najniżej −1). Za niską wartość szkicownik sam poprawia.

## Poprawianie wartości w tekście

W okienku „Tekst dla OM” można ręcznie poprawiać wartości y (druga lista), np. wpisać dokładnie 6000.
Krzywa od razu się przerysowuje.

- Dozwolone są tylko zmiany wartości y w zakresie y min – y max.
- Liczba wartości i lista x są pilnowane – x zmienia się polami „Oś x” i „Punkty”.
- Przy błędzie pojawia się czerwony komunikat, a przyciski zapisu są nieaktywne. „Przywróć” cofa do ostatniej poprawnej wersji.
- Nagłówek zawsze tworzy się od nowa, więc nie da się go zepsuć.
- Przy ręcznej poprawce wygładzanie wyłącza się samo, żeby nie zmieniało wpisanych liczb.

## Przenoszenie do OpenMusic

- **Kopiuj dla OM** – kopiuje tekst do schowka; na Macu wklej go do pudełka text-box i podłącz do `bpf-from-text`.
- **Zapisz plik .txt** – na iPhonie otwiera arkusz: „Zachowaj w Plikach” → iCloud Drive (albo AirDrop na Maca).
  Na Macu `bpf-from-text` z wejściem nil otwiera okno wyboru pliku.
- Wyjście `bpf-from-text` podłącz do **pierwszego** wejścia pudełka BPF (self).

Format tekstu:

```
;; bpf-pad: center  (precyzja 0)
(0 1 2 ... 127)
(6000 6040 ... )
```

## Aktualizacja strony

Po zmianie plików podnieś w `sw.js` numer wersji o jeden (np. `szkicownik-bpf-v11` → `v12`), wgraj zmienione pliki
(Add file → Upload files → Commit changes). Z internetem szkicownik zawsze pobiera najnowszą wersję
(bez internetu korzysta z zapamiętanej), więc po aktualizacji wystarczy go otworzyć.

---

## Szkicownik nut

Piano roll do rysowania melodii palcem lub rysikiem (iPhone, iPad, Mac) i przenoszenia jej do OpenMusic
jako chord-seq (pudełko `chseq-from-text` z biblioteki My_functions) albo do Cubasis/Cubase jako plik MIDI.

Adres: https://cywinskitomek-gh.github.io/szkicownik-bpf/nuty/
Instalacja na iPhonie: Safari → Udostępnij → „Do ekranu początkowego”; raz otwórz z internetem, potem działa też bez sieci.

### Obsługa

- **Jeden palec** rysuje nuty po siatce kwantyzacji (melodia jednogłosowa – nowa nuta zastępuje starą w tym samym miejscu).
- **Dwa palce**: rozsuwanie w poziomie powiększa czas, w pionie – wysokość wierszy; przesuwanie przewija.
- **Klawiatura z lewej**: przeciągnięcie przewija oktawy. **Linijka taktów u góry**: przeciągnięcie przewija takty.
- Na Macu: kółko/gładzik przewija (Shift – w poziomie), Ctrl + kółko (szczypanie na gładziku) powiększa.
- Okienko nad palcem pokazuje dźwięk (C3 = 6000 midicentów) i pozycję takt.miara.krok.
- **Gumka** usuwa nuty, **Cofnij** cofa ostatnie pociągnięcie, **Odtwórz** gra prostym dźwiękiem, **Pokaż wszystko** dopasowuje widok.
- „Łącz powtórzony dźwięk” – ta sama wysokość w jednym pociągnięciu daje jedną dłuższą nutę; wyłączone – osobne nuty co krok.
- „Odsłuch” – przy rysowaniu słychać rysowaną nutę, a przytrzymanie klawisza po lewej gra jego dźwięk (klawisz podświetla się na czerwono). Bezpiecznik: gdy palec stoi w miejscu dłużej niż 2 s, dźwięk gaśnie sam. Przeciągnięcie po klawiaturze nadal przewija oktawy.

### Ustawienia

Kwantyzacja (1/4, 1/8, 1/8 triola, 1/16, 1/16 triola, 1/32), tempo, metrum (ćwierćnuty w takcie), liczba taktów, velocity.

### Eksport

- **Kopiuj dla OM** / **Zapisz plik .txt** – tekst dla pudełka `chseq-from-text`:

```
;; nuty-pad: melodia  (tempo 120, metrum 4/4, velocity 100)
(6000 6400 6700)     ; wysokości, midicenty
(0 500 1000)         ; początki, ms
(500 500 1000)       ; długości, ms
```

- **Zapisz plik .mid** – MIDI (typ 0, 480 PPQ, z tempem i metrum) do Cubasis, Cubase albo OM.

### Aktualizacja

Po zmianie plików podnieś w `sw.js` numer wersji o jeden (np. `szkicownik-nut-v9` → `v10`).
