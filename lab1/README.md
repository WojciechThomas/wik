# Git i GitHub

## Podstawowa obsługa repozytorium

1. Utwórz konto na stronie https://github.com .
2. Na stronie GitHub utwórz nowe, publiczne repozytorium. Wpisz nazwę, opis i zaznacz opcję Initialize this repository with a README.
3. Dopisz parę słów do pliku README.md, następnie przesuń strone w dół, pod napisem Commit changes wpisz "Pierwsza zmiana" i zatwierdź zmiany klikając "Commit changes".
4. Wróć do strony głównej swojego repozytorium, kliknij przycisk Clone or download i skopiuj nazwę swojego repozytorium.
5. Otwórz okno linii poleceń (Term) i wpisz polecenie:
   ```text
   $git clone <https://github.com/login/repo.git>
   ```
   Po słowie `clone` wklej skopiowany wczesniej adres. W dalszej części ćwiczenia będę używał nazwy `repo` dla oznaczenia nazwy repozytorium.
6. Wejdź do sklonowanego repozytorium repo: `cd repo`
7. Zobacz stan swojego projektu: `git status`
8. Zmodyfikuj plik README.md i ponownie sprawdź stan: `gedit README.md` 
9. Dodaj zmieniony plik do zatwierdzenia: `git add README.md` i sprawdź stan - porównaj z poprzednim.
10. Zapamiętaj zatwierdzony plik w repozytorium, po opcji `-m` dopisując własny komentarz: `git commit -m "Dopisałem linijkę tekstu`
    > Jeśli nie napiszesz komentarza i uruchomi się edytor VI, to żeby z niego wyjść naciśnij: `<ESC>:q!<ENTER>` 

11. Wyślij zmiany na GitHub: `git push`  . Obejrzyj na witrynie czy wprowadzone zmiany są widoczne.
12. Skasuj lokalne repozytorium: 
    ```text
    $ cd ..
    $ rm -rf repo
    $ ls
    ```
13. Powtórz operację z p. 5., wejdź do folderu `repo` i sprawdź jego stan.
14. Tak jak wcześniej zmodyfikuj plik `README.md`, zatwierdź i zapamiętaj.
15. Obejrzyj historię swojego repozytorium:
    ```text
    $ git log
    $ git log --oneline
    $ git log --oneline --graph
    ```
    Przyjrzyj się numerom na początku każdego wpisu - identyfikują one kolejne zapisy.
16. Wróć do starej wersji repozytorium (numer w przykładzie zastąp swoim własnym, na początku linijki `Pierwsza zmiana`): `git checkout 443a0e`. Obejrzyj jak wygląda plik README.md. Wróć do aktualnej wersji projektu: `git checkout master` 
17. Wyślij zmiany na serwer.
    
## Łączenie zmian bez konfliktu

1. Upewnij się że masz tą samą wersję katalogu na komputerze i GitHubie.
2. Na stronie GitHub zmodyfikuj plik README.md i zatwierdź zmiany.
3. W katalogu `repo` dopisz nowy plik: `touch index.html`.
4. W pliku `index.html` dopisz jakiś tekst.
5. Zapamietaj plik index.html w repozytorium (add, potem commit).
6. Wyślij zmiany na serwer. Dlaczego nie udało się?
7. Pobierz zmiany z Githuba: `git pull` i obejrzyj jakie pliki są w katalogu.
   > Jeśli otworzy się edytor VI naciśnij `<ESC>:wq<ENTER>`
8. Wyślij projekt z powrotem na Github: `git push`
9. Sprawdź czy obie wersje są identyczne.

## Łączenie zmian i rozwiązywanie konflików

1. Dopisz coś w pierwszej linijce pliku README.md na stronie Github ORAZ na swoim komputerze (w każdym miejscu co innego). Zatwierdź obie zmiany.
2. Wyślij zmiany z komputera do Githuba: `git push` . Dlaczego się nie udaje?
3. Pobierz zmiany z Githuba: `git pull` . Czy wszystko jest OK?
4. Otwórz w edytorze plik README.md. Przyjrzyj sie pierwszym liniom:
   ```text
   <<<
   Zmiany z githuba
   ===
   Lokalne zmiany
   >>>
   ```
5. Usuń wszystkie "dziwne" znaczki i złącz linijki tak aby miało to sens.
6. Zapamiętaj zmieniony plik: `git commit -am "Konflikt rozwiązany"`
7. Wyślij repozytorium do Githuba: `git push`

