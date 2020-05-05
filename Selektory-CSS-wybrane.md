# Selektory CSS (wybrane)

Objaśnienia w prawej kolumnie należy czytać, dodając przed nimi frazę `Dopasowuje element` lub `Dopasowuje elementy` (nagłówek prawej kolumny).

Selektor|Dopasowuje element(y)
---|---
[attr]|z **atrybutem** o nazwie `attr`
[attr="value"]|z **atrybutem** o nazwie `attr`, którego **wartością** jest ***dokładnie*** `value`
[attr~="value"]|z **atrybutem** o nazwie `attr`, którego **wartością** są ***słowa oddzielone*** od siebie ***białymi znakami***, gdzie ***jedno*** to właśnie `value`
[attr\|="value"]|z **atrybutem** o nazwie `attr`, którego **wartość** to ***dokładnie*** `value` ***albo zaczyna się*** od `value`, ***po czym bezpośrednio jest łącznik/minus*** (`-`) (U+002D)
[attr^="value"]|z **atrybutem** o nazwie `attr`, którego **wartość** zaczyna się od `value`
[attr$="value"]|z **atrybutem** o nazwie `attr`, którego **wartość** kończy się na `value`
[attr*="value"]|z **atrybutem** o nazwie `attr`, **w** którego **wartości** występuje **ciąg** znaków `value`
... i]|... ,a **wielkość liter** w wartości atrybutu **nie ma znaczenia** (w zakresie ASCII)
`,`|wybrane przez selektory, oddzielone `,` - **działa** tylko, kiedy **wszystkie selektory** są **prawidłowe**
spacja|[przodek]spacja[`dopasowywany`]
\>|[rodzic]>[`dopasowywane bezpośrednie dziecko`]
~|[rodzeństwo wyżej w kodzie strony]~[`dopasowywany`]
+|[rodzeństwo BEZPOŚREDNIO przed w kodzie strony]+[`dopasowywany`]
:active|aktywowany przez użytkownika element; LVHA
:checked|włączone: `radio`, `checkbox` lub `option`; `option` – w pewnych przeglądarkach ograniczone możliwości ostylowania
:focus|kliknięty lub wybrany przy pomocy klawisza `Tab` na klawiaturze
:focus-within|element, który ma `:focus` lub który zawiera element, który ma `:focus`
:hover|nad którym jest kursor myszy; jeśli urządzenie dotykowe: bardzo różna obsługa; LVHA
:not()|który nie pasuje do selektora podanego w nawiasie; nie używać pseudoelementów; nie wolno zagnieżdżać tej pseudoklasy: `:not(:not(...))`; lista argumentów w nawiasie nie jest szeroko zaimplementowana!
:link|każdy nieodwiedzony `a`, `area` lub `link`, który ma atrybut `href`; LVHA
:visited|każdy odwiedzony link; ograniczone właściwości z uwagi na prywatność; LVHA
:target|jeśli jest on celem aktualnie użytego łącza wewnętrznego
:nth-child()|spośród węzłów o **wspólnym rodzicu**, o pozycji określonej liczbą w nawiasie (numeracja od `1`) która może być postaci: `An+B`, gdzie `A`,`B` to dziesiętne liczby całkowite; można pominąć część `An+` lub `+B` – pominięte części są uznawane za `0`; `A` może być równe `-1`, wtedy `1` można pominąć; `B` może być ujemne, wtedy trzeba zastąpić znak `+` znakiem `-`; `n` automatycznie przybiera wartości od `0` w górę
:nth-last-child()|to samo co `:nth-child()`, jedyna różnica: numeracja pozycji od tyłu
:nth-of-type()|spośród węzłów **tego samego typu o wspólnym rodzicu** (**LEPSZY OD `:nth-child()`**) o pozycji określonej liczbą w nawiasie - składnia identyczna jak w `:nth-child()`
:nth-last-of-type()|to samo co `:nth-of-type()`, jedyna różnica: numeracja pozycji od tyłu
::before|tworzy niezaznaczalne dziecko danego elementu PRZED nim, które objęte jest formatowaniem tego elementu, włącznie z kwestią widoczności. Składnia - poniżej
::after|identyczny do `::before`, jedyna różnica: dodaje specyficzne dziecko PO elemencie

LVHA - Reguła LVHA: `:link`, `:visited`, `:hover`, `:active` – kolejność umieszczania w kodzie CSS pseudoklas związanych z łączem, w kolejności: od lewej
# Składnia `::before/::after`
###### Na przykładzie `::after` - dla `::before` identycznie
[`selektor elementu`]::after
{

white-space: pre-wrap; /* `DOPIERO USTAWIENIE tej właściwości NA TĘ WARTOŚĆ daje wolność w kwestii przełamywania linii oraz odstępów, przełamanie linni gdy kończy się miejsce w wierszu` */

content: "`zawartość tekstowa`";

color: `kolor tekstu`;

}

## Zawartość
dopuszczalne możliwości (do użycia także jednocześnie - rozdzielane spacjami):
### String
- podawany w pojedynczym albo podwójnym cudzysłowie (jeden typ nie może zawierać się w fragmencie ograniczonym drugim typem, chyba że poprzedzony znakiem `\`)
- oznaczenie nowej linii: `\a`
- uzyskanie znaku specjalnego - `\[kod znaku w Unicode]`, np. `\2190` - strzałka w lewo
### url
wskazuje zewnętrzny zasób, adres URL umieścić jak `String`, URL może być bezwzględny lub względny; gdy względny - wtedy bazowym URL jest adres arkusza stylów a nie dokumentu źródłowego
### attr(X)
zwraca jako `String` wartość **atrybutu** `X` podmiotu selektora, jeśli podmiot selektora nie ma takiego atrybutu, zwracany jest pusty ciąg, wrażliwość na wielkość znaku zależy od języka dokumentu
### counters()
wyświetla ciąg znaków zawierający wartości zagnieżdżonych liczników o podanej nazwie (jeśli istnieją), od najbardziej zewnętrznego do najbardziej wewnętrznego, oddzielając te wartości określonym przez użytkownika `String`iem, jeśli taki istnieje; `counters()` przyjmuje parametry:
- nazwę licznika, w której ważna jest wielkość liter, musi być taka sama dla resetowania licznika i jego zwiększania, nie może zaczynać się od 2 myślników;
- `String` o dowolnej długości oddzielający od siebie wartości licznika, znaki nie łacińskie muszą być zakodowane przy użyciu sekwencji ucieczki, np. `\000A9`;

`counters()` do działania wymaga jeszcze:
- stworzenia licznika za pomocą `counter-reset`:
1. zawiera nazwę lub nazwy liczników, które te liczniki są resetowane dla każdego wystąpienia elementu HTML, dla którego przypisano ten `counter-reset` w arkuszu CSS
2. liczniki te są resetowane domyślnie do `0`, chyba że po nazwie licznika jest podana wartość całkowita – może być ujemna – wtedy resetuje do tej wartości licznik, którego nazwa jest przed tą wartością, jeżeli licznik o danej nazwie nie istnieje, to zostaje stworzony
3. wszystkie nazwy i wartości należy oddzielić od siebie spacją

- oraz jego zwiększenia za pomocą `counter-increment`:
1. zawiera nazwę lub nazwy liczników, które te liczniki są zwiększane dla każdego wystąpienia elementu HTML, dla którego przypisano ten `counter-increment` w arkuszu CSS
2. liczniki te są domyślnie zwiększane o `1`, chyba że po nazwie licznika jest podana wartość całkowita – może być ujemna – wtedy zwiększa o tę wartość licznik, którego nazwa jest przed tą wartością
3. wszystkie nazwy i wartości należy oddzielić od siebie spacją

Polecenie resetowania dla elementu można nadpisać tzn. że będzie wykonane tylko ostatnie polecenie resetowania.

Właściwości `counters()`:

Wartości liczników dla jednego elementu są:
- wyświetlane po zresetowaniu/zwiększeniu;
- najpierw resetowane, później zwiększane.

Zasięg licznika rozpoczyna się od pierwszego elementu w dokumencie, na którym zresetowano ten licznik i obejmuje potomków tego elementu oraz jego rodzeństwo wraz z ich potomkami. Nie obejmuje jednak żadnych elementów w zakresie licznika o tej samej nazwie utworzonej przez zresetowanie licznika w rodzeństwie elementu lub przez późniejsze zresetowanie licznika tego samego elementu.
Jeżeli `counter-increment` lub `content` elementu lub pseudoelementu odnosi się do licznika, który nie jest objęty jakimkolwiek zresetowaniem licznika, powinno nastąpić zresetowanie licznika do 0 dla tego elementu lub pseudoelementu.
Jeżeli element ma ustawioną właściwość `display` na `none`, licznik nie może zostać zmieniony ani zresetowany. Nie dotyczy to ustawienia właściwości `visible` na `hidden`.

# Przykłady użycia wybranych selektorów
Selektor|Dopasowuje
---|---
a[href*="tekst" i]|`a`, który w wartości atrybutu `href` ma ciąg liter `tekst` zapisany DOWOLNĄ wielkością
body :not(div):not(span)|wszystko w `body` oprócz `div` i `span`
body :not(table) a|linki m.in. w tabeli, bo `td` pasuje do `:not(table)`
:nth-child(7)|każde 7. dziecko
:nth-child(5n)|każde co 5. dziecko
:nth-child(3n+4)|każde 4., 7., 10. ... dziecko
:nth-child(-n+3)|każde pierwsze 3 dzieci
a:nth-child(n+8):nth-child(-n+15)|każde od 8. do 15. włącznie dziecko, które musi być `a`
p:nth-of-type(2n+1)|nieparzyste paragrafy
p:nth-of-type(2n)|parzyste paragrafy
p:nth-of-type(1)|1. paragraf
p:nth-of-type(4n)|co 4. paragraf

## Przykład użycia ::before/::after

h1::before

{

content: "Rozdział " counter(chapter) ". ";

}

h2:before

{

content: counter(chapter) "." counter(section) " ";

counter-increment: section;

}

---

div.x::after

{

content: counters(item, ".");

}

# Przyszłość
Selektory, które dołączę do niniejszego zestawienia po ich wdrożeniu:
`:has()`, `||`

[źródło](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
