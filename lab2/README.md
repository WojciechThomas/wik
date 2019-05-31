# Lab 2 - Vagrant - szybka konfiguracja maszyn wirtualnych

Do wykonania ćwiczeń z laboratorium potrzebujesz zainstalowanych aplikacji: VirtualBox i Vagrant. Obie aplikacje istnieją w wersjach dla systemów Linux, Windows, Mac.

## Pobranie maszyny 

1. Przed rozpoczęciem pracy pobierz obraz maszyny: `vagrant box add chenhan/lubuntu-desktop-18.04`

## Uruchamianie maszyny

1. Przejdź do katalogu `wik/lab2`. Obejrzyj w edytorze plik Vagrantfile
2. Utwórz nową maszynę wirtualną przy użyciu aplikacji Vagrant:
   ```text
   $ vagrant up
   ```
   Poczekaj aż maszyna zakończy całą instalację.
3. Gbędzie widoczny będzie z powrotem znak zachęty `$` uruchom przeglądarkę i otwórz stronę `http://localhost:8080/`.
4. Jeśli zobaczyłeś ekran powitalny serwera Apache - gratulacje, możesz iść dalej.
5. Otwórz w edytorze plik `wik/lab2/html/index.html`. Zmień jego zawartość i sprawdź czy wprowadzone zmiany są od razu widoczne w przeglądarce.
6. Dodaj plik `wik/lab2/html/test.html`, zapisz w nim jakąś zawartość, a następnie spróbuj otworzyć w przeglądarce stronę: `http://localhost:8080/test.html`
7. Obejrzyj odpowiedzi serwera www przy pomocy programu `curl`:
```
$ curl http://localhost:8080/
$ curl http://localhost:8080/test.html
```
Wybrane polecenia uruchom ponownie z dodaną opcją `-v`
8. Połącz się z maszyną Vagrant protokołem ssh:
   1. Z poziomu projektu Vagrant: w katalogu `wik/lab2` uruchom polecenie . Obejrzyj adres IP serwera, jego nazwę:
   ```text
   $ vagrant ssh
   vagrant@vagrant:~$ ip ad
   vagrant@vagrant:~$ hostname
   vagrant@vagrant:~$ logout
   ```
   2. Z poziomu systemu gospodarza (hasło: vagrant):
   ```text
   $ ssh vagrant@localhost -p 2222
   vagrant@vagrant:~$ ip ad
   vagrant@vagrant:~$ hostname
   vagrant@vagrant:~$ logout
   ```
9. Usuń maszynę z dysku i pamięci: `vagrant destroy -f`
10. Utwórz maszynę na nowo: `vagrant up` i sprawdź czy działa tak samo jak poprzednia.
11. Zatrzymaj maszynę przez `vagrant halt` i włącz ponownie przez `vagrant up`

## Modyfikacja działania serwera Apache

1. Wykonaj polecenie `vagrant ssh`.
2. Będąc w maszynie wirtualnej zmodyfikuj plik konfiguracyjny serwera Apache:
   ```text
   sudo nano /etc/httpd/conf/httpd.conf
   ```
   nano to prosty edytor tekstu, a jego dwa najważniejsze polecenia to: Ctrl-O - zapis pliku, Ctrl-X - wyjście.
3. Przed restartem serwera w celu uwzglęnienia zmian, sprawdź czy nie zrobiłeś w pliku httpd.conf błędów (i popraw je przed restartem serwera):
   ```text
   sudo apachectl configtest
   ```
   Jeśli wszystko jest OK, uruchom ponownie serwer, aby uwzglednić zmiany:
   ```text
   sudo apachectl restart
   ```
4. W pliku `httpd.conf` dodaj następujące dyrektywy (poniżej sekcji `<Directory /var/www/html>...</Directory>`):
   ```text
   Alias /ten /vagrant/tamten
   <Location /ten>
     Options Indexes FollowSymLinks
     Require all granted
   </Location>
   ```
   Teraz wszystkie zapytania kierowane pod adresem `http://localhost:8080/ten` pobierają tak naprawdę zawartość z folderu `tamten`.

## Nowa, własna maszyna

1. Utwórz folder na nowy projekt:
   ```text
   $ cd ..
   $ mkdir lab2a
   $ cd lab2a
   $ vagrant init chenhan/lubuntu-desktop-18.04
   $ vagrant up
   ...
   $ vagrant ssh
   ```
2. Sprawdź czy w maszynie jest serwer Apache
3. Zatrzymaj maszynę `vagrant halt`
4. Otwórz w edytorze plik `lab2a/Vagrantfile`
5. Obejrzyj sekcję `config.vm.provision`. Usuń komentarze (`#`) sprzed CAŁEJ sekcji, włącznie z linią `SHELL`.
6. Uruchom maszynę `vagrant up`
7. Czy w maszynie jest serwer Apache?
8. Uruchom polecenie `vagrant provision`
9. Czy w maszynie jest serwer Apache?
