# 🎮 Familiada — Instrukcja obsługi

Przeglądarkowa wersja polskiej Familiady na imprezę domową. Nie wymaga instalacji ani połączenia z internetem — wystarczy otworzyć plik w przeglądarce.

---

## Zawartość repozytorium

```
familiada.html              ← główny plik gry (otwórz w przeglądarce)
familiada_pytania.json      ← pytania i odpowiedzi (edytuj dowolnie)
familiada_odpowiedzi.csv    ← surowe dane z ankiety (do wglądu)
sounds/                     ← folder na pliki dźwiękowe (opcjonalny)
  odpowiedz.mp3             ← dźwięk odkrycia odpowiedzi
  blad.mp3                  ← dźwięk błędu (X)
  steal.mp3                 ← dźwięk podkradzenia
  buzzer.mp3                ← dźwięk naciśnięcia buzzera
  koniec.mp3                ← dźwięk końca rundy
README.md                   ← ten plik
```

---

## Uruchomienie

1. Pobierz całe repozytorium (lub przynajmniej `familiada.html` i `familiada_pytania.json`) do jednego folderu.
2. Otwórz `familiada.html` w przeglądarce (Chrome / Firefox / Edge — wszystkie działają).
3. Na ekranie startowym kliknij **„Wczytaj pytania (JSON)"** i wskaż plik `familiada_pytania.json`.
4. Opcjonalnie wczytaj dźwięki (patrz sekcja [Dźwięki](#dźwięki)).
5. Graj!

> **Uwaga:** plik HTML musi znajdować się w tym samym folderze co `familiada_pytania.json` oraz folder `sounds/`, żeby względne ścieżki działały poprawnie.

---

## Zasady gry

Gra przeznaczona dla **dwóch drużyn** (po dowolnej liczbie graczy). Prowadzący obsługuje grę z klawiatury lub klikając przyciski na ekranie.

### Przebieg rundy

1. **Pytanie** pojawia się na środkowym pasku. Odpowiedzi są ukryte.
2. **Buzzer** — obaj kapitanowie drużyn stają przy klawiaturze (lub dotykają ekranu). Kto pierwszy naciśnie swój przycisk, zdobywa prawo pierwszego słowa.
   - Drużyna 1: klawisz `Q`
   - Drużyna 2: klawisz `P`
3. **Grająca drużyna** próbuje odgadnąć ukryte odpowiedzi jedna po jednej. Prowadzący odkrywa poprawne odpowiedzi klawiszami `1`–`9`.
4. Za każdą **błędną odpowiedź** prowadzący naciska `X` — na ekranie pojawia się czerwone „X". **Trzy błędy** kończą grę dla aktywnej drużyny i uruchamiają **podkradzenie**.
5. **Podkradzenie** — drużyna przeciwna ma jedną szansę na podanie dowolnej odpowiedzi:
   - Jeśli trafi → zdobywa wszystkie punkty rundy.
   - Jeśli spudłuje → punkty wracają do drużyny grającej.
6. Jeśli drużyna odkryje **wszystkie odpowiedzi** bez trzech błędów — runda kończy się natychmiast i zdobywa całą pulę punktów.
7. Po rundzie punkty są doliczane, a gra przechodzi do kolejnego pytania.

### Punktacja

Każda odpowiedź ma przypisaną liczbę punktów (widoczną po odkryciu). Suma punktów w rundzie wynosi zawsze **100**. Wartości odpowiadają procentowi ankietowanych, którzy danej odpowiedzi udzielili.

Wygrywa drużyna z wyższym łącznym wynikiem po wszystkich rundach.

---

## Sterowanie — skróty klawiszowe

| Klawisz | Akcja |
|---------|-------|
| `Q` | Buzzer — Drużyna 1 |
| `P` | Buzzer — Drużyna 2 |
| `1` – `9` | Odkryj odpowiedź o danym numerze |
| `X` | Dodaj błąd (czerwone X) |
| `Tab` | Ręczna zmiana aktywnej drużyny |
| `Spacja` | Przyznaj punkty rundy aktywnej drużynie (bez czekania na odkrycie wszystkich) |
| `R` | Następna runda (po wyświetleniu ekranu końca rundy) |

> Skróty są widoczne w dolnej części ekranu gry jako podpowiedź dla prowadzącego.

---

## Edycja pytań i odpowiedzi

Plik `familiada_pytania.json` możesz edytować w dowolnym edytorze tekstu (np. Notepad++, VS Code, Zed).

### Struktura pliku

```json
{
  "_instrukcja": "...",
  "pytania": [
    {
      "pytanie": "Treść pytania widoczna na ekranie",
      "odpowiedzi": [
        { "tekst": "Najczęstsza odpowiedź", "punkty": 45 },
        { "tekst": "Druga odpowiedź",       "punkty": 25 },
        { "tekst": "Trzecia odpowiedź",     "punkty": 18 },
        { "tekst": "Czwarta odpowiedź",     "punkty": 12 }
      ]
    }
  ]
}
```

### Zasady edycji

- **Suma punktów** w każdym pytaniu powinna wynosić **100**. Gra działa też bez tej zasady, ale tablica wyników będzie nieczytelna.
- Odpowiedzi powinny być ułożone **od najczęstszej do najrzadszej** — pojawią się na tablicy w tej kolejności.
- Liczba odpowiedzi na pytanie: **od 2 do 9** (więcej nie zmieści się na tablicy dwukolumnowej).
- Pytania są rozgrywane **w kolejności** z pliku.

### Przykład własnego pytania

```json
{
  "pytanie": "Co zabierasz na plażę?",
  "odpowiedzi": [
    { "tekst": "Ręcznik",     "punkty": 38 },
    { "tekst": "Krem do opalania", "punkty": 27 },
    { "tekst": "Okulary słoneczne", "punkty": 18 },
    { "tekst": "Książka / telefon", "punkty": 10 },
    { "tekst": "Woda / napoje", "punkty": 7 }
  ]
}
```

---

## Dźwięki

Gra obsługuje opcjonalne pliki dźwiękowe. Działają **dwa sposoby** ich wczytania:

### Sposób 1 — automatyczny (zalecany)

Umieść pliki w podfolderze `sounds/` obok `familiada.html`. Nazwy muszą być dokładnie takie:

| Plik | Kiedy gra |
|------|-----------|
| `sounds/buzzer.mp3` | Naciśnięcie buzzera przez gracza |
| `sounds/odpowiedz.mp3` | Odkrycie poprawnej odpowiedzi |
| `sounds/blad.mp3` | Błąd (X) |
| `sounds/steal.mp3` | Uruchomienie podkradzenia (po 3 błędach) |
| `sounds/koniec.mp3` | Koniec rundy / przyznanie punktów |

Gra wczyta je automatycznie przy starcie. Zielona kropka obok nazwy na ekranie startowym oznacza, że plik został wykryty.

### Sposób 2 — ręczny

Na ekranie startowym kliknij **„Wczytaj dźwięki"** i wskaż dowolne pliki audio z dysku. Gra rozpozna je po nazwie — plik zawierający słowo `buzzer`, `blad`, `odpowiedz`, `steal` lub `koniec` zostanie przypisany do odpowiedniej akcji.

Obsługiwane formaty: `.mp3`, `.ogg`, `.wav`, `.m4a`.

> Dźwięki są całkowicie opcjonalne — gra działa bez nich.

---

## Ustawienie sprzętowe na imprezie

Zalecany układ dla maksymalnego efektu:

```
[Telewizor / duży monitor]
         ↑
    [Laptop prowadzącego]
    klawiatura przed ekranem

[Gracz D1]          [Gracz D2]
  klawisz Q           klawisz P
  (lewa strona        (prawa strona
   klawiatury)         klawiatury)
```

- Podłącz laptop do telewizora przez HDMI i ustaw tryb **duplikowania** ekranu.
- Gracze stają po obu stronach laptopa i trzymają palec nad swoim klawiszem buzzera.
- Prowadzący obsługuje resztę klawiszy (`1`–`9`, `X`, `Tab`, `Spacja`).

Alternatywnie można użyć zewnętrznej klawiatury lub pada — gra reaguje na standardowe zdarzenia klawiatury.

---

## Znane ograniczenia

- Gra nie zapisuje wyników między sesjami — po zamknięciu przeglądarki wynik resetuje się.
- Brak timera dla graczy — prowadzący decyduje, kiedy odpowiedź jest za długa.
- Plik HTML wymaga dostępu do internetu przy pierwszym uruchomieniu, aby wczytać czcionkę Oswald z Google Fonts. Przy braku internetu gra działa poprawnie, ale z czcionką zastępczą.
- Może być tak że gracze wcisną buzzer (q lub p), żeby odpowiedzieć pierwsi ale nie odpowiedzą poprawnie i pytanie przechozi na drugą drużynę (jeśli reprezentant odpowiedział poprawnie). W takim przypadku kontunuuj rundę, ale na końcu, po trzech stratach drużyna pierwsza będzie mogła zabrać punkty, kliknij na odwrót (Trafili zamiast Pudło, Pudło zamiast Trafili). Kiedyś to fixne ale tera mi się nie chce.

---

## Licencja

Projekt open-source — możesz go dowolnie modyfikować, kopiować i używać na niekomercyjnych imprezach. Pytania zawarte w `familiada_pytania.json` pochodzą z ankiety przeprowadzonej na potrzeby konkretnej imprezy i możesz je zastąpić własnymi.
