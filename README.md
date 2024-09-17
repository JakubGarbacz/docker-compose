1. (Docker) W jaki sposób można sprawdzić czy nasza aplikacja działa i nasłuchuje na danym porcie?

docker ps    #wyświetla listę uruchomionych kontenerów wraz z portami

CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                  NAMES
8964c1801deb   nginx     "/docker-entrypoint.…"   16 seconds ago   Up 15 seconds   0.0.0.0:8080->80/tcp   nginx

docker exec -it nginx curl localhost:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

curl localhost:8080

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
-------------------------------------------------------------------------
2. Jaka jest różnica pomiędzy docker exec a docker run?

docker run -it nginx /bin/bash  # Tworzy nowy kontener z obrazem Nginx i uruchamia bash

docker exec -it 8964c1801deb /bin/bash  # Uruchamia bash w istniejącym kontenerze
-------------------------------------------------------------------------
3. Jaka jest różnica pomiędzy ENTRYPOINT a CMD w Dockerfile?

CMD: Służy do ustawienia domyślnej komendy, która zostanie uruchomiona, gdy użytkownik nie poda żadnej innej komendy podczas uruchamiania kontenera

CMD ["echo", "Welcom"]

ENTRYPOINT: Definiuje komendę, która zawsze zostanie uruchomiona, niezależnie od tego, czy użytkownik poda inną komendę przy uruchamianiu kontenera. Komenda podana przez użytkownika staje się argumentem dla ENTRYPOINT

ENTRYPOINT ["echo]
Różnica polega na tym, że ENTRYPOINT definiuje stałą komendę, a CMD pozwala na jej nadpisanie.
-----------------------------------------------------------------------
4. Co to jest Docker Swarm?

Docker Swarm to narzędzie do orkiestracji kontenerów
Tworzenie klastra z wielu maszyn i uruchamianie kontenerów w sposób rozproszony
Automatyczne skalowanie kontenerów
Równoważenie obciążenia (load balancing).

docker swarm init  # Inicjalizacja Swarm
docker service create --name my_service --replicas 3 nginx  # Tworzenie usługi z 3 replikami
---------------------------------------------------------------------
5. Co sprawdzić, gdy linuxowa maszyna zaczyna spowalniać?

Sprawdź zużycie zasobów systemowych:
top lub htop dla procesora i pamięci
df -h dla przestrzeni dyskowej
iostat dla I/O dysku
free -m dla pamięci RAM
dmesg dla logów systemowych
----------------------------------------------------------------------
6. Jak zliczyć ilość wystąpień ciągu 'XXX' w pliku binarnym?

Można użyć narzędzia grep z opcją -a (treat binary as text) i -o (only matching).
grep -a -o 'XXX' plik.bin | wc -l
----------------------------------------------------------------------
7. Jak utworzyć plik w Linuxie o wielkości 1KB zawierający losowe dane?

Można użyć polecenia dd z /dev/urandom

dd if=/dev/urandom of=plik.bin bs=1K count=1

if=/dev/urandom oznacza źródło losowych danych
bs=1K ustawia wielkość bloku na 1 KB
count=1 oznacza, że zostanie wygenerowany tylko jeden blok
----------------------------------------------------------------------
8. Czy ciąg „218.2.1” jest poprawnym adresem IP?

Nie, poprawny adres IPv4 składa się z czterech oktetów (np. 192.168.1.1).
-----------------------------------------------------------------------
9. Co można zrobić, gdy przy wydawaniu polecenia „rm nazwa_pliku” uzyska się błąd „brak dostępu”? Jakie mogą być przyczyny?

Możliwe przyczyny:
Brak uprawnień: użyj sudo rm nazwa_pliku.
Plik jest chroniony przed zapisem: sprawdź uprawnienia ls -l nazwa_pliku i zmień je chmod u+w nazwa_pliku.
-----------------------------------------------------------------------
10. W jaki sposób usunąć wszystkie pliki, których nazwa zaczyna się od znaku „-”?

rm -- -nazwa_pliku
-----------------------------------------------------------------------
11. Na jakim porcie działa narzędzie ping?

ping nie działa na żadnym porcie gdyż nie używa protokołów TCP ani UDP
ping używa protokołu ICMP(Internet Control Message Protocol) który nie ma przypisanego numeru portu
-----------------------------------------------------------------------
12. W katalogu znajduje się kilkaset tysięcy plików. Jak usunąć je wszystkie?

rm -rf /ścieżka/do/katalogu/*
-----------------------------------------------------------------------
13. Co się stanie, gdy skasujemy plik, do którego zapisuje uruchomiona aplikacja?

Plik zostanie usunięty z systemu plików, ale dane będą nadal dostępne dla aplikacji do momentu zamknięcia pliku przez aplikację.
-----------------------------------------------------------------------
14. W jaki sposób wyświetlić otwarte pliki znajdujące się w podkatalogach /home?

lsof +D /home
find /home -type f -exec lsof {} +
----------------------------------------------------------------------
15. aHR0cDovL3dlbHRpZ28uY29tL3JlY3J1aXRtZW50Lwo=

To jest zakodowany ciąg Base64. Po dekodowaniu otrzymujemy: 
http://weltigo.com/recruitment/.

echo "aHR0cDovL3dlbHRpZ28uY29tL3JlY3J1aXRtZW50Lwo=" | base64 --decode
http://weltigo.com/recruitment/

python script

import base64

encoded_str = "aHR0cDovL3dlbHRpZ28uY29tL3JlY3J1aXRtZW50Lwo="
decoded_bytes = base64.b64decode(encoded_str)
decoded_str = decoded_bytes.decode('utf-8')

print(decoded_str)
http://weltigo.com/recruitment/

