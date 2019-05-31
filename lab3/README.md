# Lab 3 - Docker - szybka konfiguracja kontenerów

## Uruchamianie maszyny

1. Przejdź do katalogu `wik/lab3`. 
2. Utwórz nową maszynę wirtualną przy użyciu aplikacji Vagrant:
   ```text
   $ vagrant up
   ```
   Poczekaj aż maszyna zakończy całą instalację.
3. Obejrzyj w edytorze plik Vagrantfile i porównaj go z poprzednim laboratorium.

## Pierwsze kontenery

1. Połącz się z serwerem Vagrant: `vagrant ssh`
2. Przejdź do folderu `/vagrant`: `cd /vagrant`
3. Wyświetl wersję środowiska Docker: `docker --version`
4. Uruchom pierwszy kontener, wyświetl listę obrazów i zobacz listę kontenerów w systemie:
   ```text
   $ docker run hello-world
   $ docker image ls
   $ docker container ls -all
   ```
5. Uruchom testowo kontenery popularnych systemów :
   ```text
   $ docker run --rm -ti ubuntu:latest /bin/ bash
   $ docker run --rm -ti fedora:latest /bin/ bash
   $ docker run --rm -ti centos:latest /bin/ bash
   ```
   Za każdym razem zobacz nazwę maszyny: `hostname` i zakończ pracę przez `<Ctrl-D>`, dodatkowo możesz przetestować więcej opcji:
   ```text
   uname -r
   cat /etc/os-release
   yum update (fedora/centos) 
   apt-get update (ubuntu)
   ```

## Uruchomienie serwera Apache w kontenerze

1. Uruchom kontener z serwerem Apache:
   ```text
   $ docker run -d --name myapache -p 8080:8080 bitnami/apache
   ```
   Zobacz w przeglądarce czy serwer działa wchodzą na stronę: `http://localhost:8080`
2. Wyświetl listę działających kontenerów, zatrzymaj kontener myapache i usuń kontener z pamięci:
   ```text
   $ docker ps
   $ docker stop 34ef1
   $ docker ps
   $ docker ps -a
   $ docker rm 34ef1
   ```
   Identyfikator 34ef1 zastąp identyfikatorem swojego kontenera.
3. Uruchom kontener podłączając folder gospodarza:
   ```text
   $ docker run -d --name myapache -p 8080:8080 -p 8443:8443 -v /vagrant:/app bitnami/apache
   ```
   Usuń kontener jak poprzednio, ale teraz zamiast identyfikatora użyj nazwy obrazu `myapache`, np. `docker stop myapache`
   Otwórz w przeglądarce strony: `http://localhost:8080/` i `https://localhost:8443`

## Budowa własnego kontenera

1. Obejrzyj plik Dockerfile definiujący co ma zawierać nowy kontener
2. Zbuduj kontener użwając pliku Dockerfile i uruchom go:
   ```text
   $ cd /vagrant
   $ docker built -t myapacheimage .
   $ docker run -d -p 8080:8080 myapacheimage
   ```
   Zobacz że tym razem nowy kontener nie jest łączony z systemem plików (opcja `-v`) a mimo to udostępnia naszą stronę.
3. Zatrzymaj kontener i usuń go.

## Uruchomienie całej usługi

1. Obejrzyj plik `docker-compose.yml` definiujący działanie kontenera.
2. Uruchom kontener korzystając z aplikacji `docker-compose`:
   ```text
   $ docker-compose up -d
   $ curl http://localhost:8080
   $ docker-compose down
   ```
   Zamiast polecenia `curl` możesz otworzyć przeglądarkę i sprawdzić działanie strony
4. Przejdź do folderu wordpress i zbuduj kontener obslugujący Wordpressa:
   ```text
   $ cd /vagrant/wordpress
   $ docker-compose up -d
   ... otwórz w przeglądarce stronę http://localhost:8080
   $ docker-compose down
5. Przejrzyj plik docker-compose.yml:
   - na ilu kontenerach działa Wordpress?
   - z jakich obrazów jest zbudowany?
   - gdzie są przechowywane dane Wordpressa?




