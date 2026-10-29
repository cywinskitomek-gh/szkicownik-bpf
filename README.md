# Szkicownik BPF

Rysowanie krzywych palcem lub rysikiem (iPhone, iPad, Mac) i przenoszenie ich do OpenMusic jako BPF.
Autor: Tomasz Cywiński. Wczytywanie w OM: pudełko `bpf-from-text` z biblioteki My_functions.

Adres: https://cywinskitomek-gh.github.io/szkicownik-bpf/

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

Po zmianie plików podnieś w `sw.js` numer wersji (`szkicownik-bpf-v10` → `v11`), wgraj zmienione pliki
(Add file → Upload files → Commit changes). Na iPhonie otwórz szkicownik z internetem; jeśli pokaże starą
wersję, zamknij go i otwórz ponownie.
