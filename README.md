# AzureIllusion dla Jellyfin

Plugin dostarcza polskie napisy z API AzureIllusion do Jellyfin. Strona i API
AzureIllusion nadal używają wyłącznie identyfikatorów AniList. Identyfikatory
Kitsu lub AniDB mogą zostać przetłumaczone na AniList tylko lokalnie, w
konfiguracji pluginu.

## Zgodność

- Jellyfin Server 10.11.11
- .NET 9
- formaty napisów: ASS i SRT
- oznaczenia języka: PL i PL2
- seriale, odcinki specjalne (w tym odcinek 0) oraz filmy

## Instalacja ręczna

1. Rozpakuj `AzureIllusion_0.1.0.0.zip` do katalogu pluginów Jellyfin, do nowego
   folderu `AzureIllusion`.
2. Uruchom ponownie Jellyfin.
3. Otwórz `Panel administracyjny > Wtyczki > AzureIllusion`.
4. Ustaw adres API `https://subs.azureillusion.ovh`, klucz API i zapisz.
5. W konfiguracji biblioteki włącz provider napisów AzureIllusion.

## Dopasowanie anime

Kolejność dopasowania jest celowo zachowawcza:

1. identyfikator AniList zapisany w Jellyfin,
2. lokalne mapowanie `Kitsu -> AniList` lub `AniDB -> AniList` z konfiguracji,
3. dokładne dopasowanie znormalizowanego tytułu i roku przez API AzureIllusion.

Wynik niejednoznaczny jest pomijany. Plugin nigdy nie przesyła identyfikatorów
Kitsu ani AniDB do strony AzureIllusion.

## Wybór napisów

Można pobierać najlepiej ocenione wydania albo ograniczyć wyniki do wybranych
grup pobieranych dynamicznie z API. Dostępne są również: minimalna ocena,
wyłącznie zweryfikowane wydania, limit liczby grup oraz automatyczne pobieranie.

Plugin zapamiętuje pobrane wydania na podstawie identyfikatora i sumy kontrolnej,
aby nie pobierać ponownie tego samego pliku dla tej samej pozycji biblioteki.

## Bezpieczeństwo

- używaj wyłącznie adresu API HTTPS,
- utwórz osobny klucz API dla Jellyfin,
- nie umieszczaj klucza w logach ani publicznych zgłoszeniach,
- po ujawnieniu klucza unieważnij go w panelu AzureIllusion.

## Budowanie

```powershell
.\build-plugin.ps1
```

Skrypt uruchamia testy, buduje wydanie i zapisuje ZIP oraz plik SHA-256 w
folderze `artifacts`.
