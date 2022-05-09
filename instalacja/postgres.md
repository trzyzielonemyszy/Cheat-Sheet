VM wymagania:

przynajmniej 80 GB wolnego miejsca na root

![1a4040a493fd61ab063da2c567bd0096.png](:/6d4e65c38725469f85b5b188f7925773)

**instalacja postgresa v14:**

instalacje repo RPM:

`sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm`

instalacja postgresSQL v14:

`sudo yum install -y postgresql14-server`

inicjalizacja bazy i włączenie autostartu:

`sudo /usr/pgsql-14/bin/postgresql-14-setup initdb`
`sudo systemctl enable postgresql-14`
`sudo systemctl start postgresql-14`

**konfiguracja**

postgresql.conf:

`vim /var/lib/pgsql/14/data/postgresql.conf`

![319d7b836157422f888cd01a9fe76a9e.png](:/15f4ba31ef6e4211a5d38536ed8af6d4)

listen_adresses = '==ip vm na której stawiany jest postgres server=='

pg_hba.conf:

`vim /var/lib/pgsql/14/data/pg_hba.conf`

![00e81f6155f98b709ade2fd51dd68f4a.png](:/2adadd8d080b438a93cd7dba2d1ed950)

uzupełnij brakujące hosty:

\# TYPE DATABASE USER ADDRESS METHOD

`# IPv4 local connections:`

`host all all 127.0.0.1/32 ident`

`host all all ::1/128 ident`

`host all all 10.55.1.0/24 md5 #okd`

`host all all 127.0.0.1/32 md5 #local`

`host all all ==server_ip==/32 trust #` `!!! póki co 'trust', po przypisaniu hasła zmiana na md5`

`host all postgres ==server_ip==/32 md5`

`host all all 10.0.15.0/24 md5 #vpn atm full`

`host all all 10.55.1.221/32 md5`

zapisz i wyjdź z vima

`:wq`

restart serwisu:

`systemctl restart postgresql-14`

!serwis trzeba restartować po każdej zmianie w plikach pg_hba.conf i postgresql.conf!

otwórz port dla postgresa

```
firewall-cmd --zone=public --add-port=5432/tcp --permanent

```

```
firewall-cmd --reload
```

zaloguj sie do postgresa na użytkownika postgres:

`psql -U postgres -h ==ip_serwera==`

ustaw hasło dla użytkownika postgres:

`postgres=# \password postgres`

`Enter new password: ==<new-password>==`

`postgres=# \q`

zmień rodzaj autoryzacji w pg_hba.conf na md5

`vim /var/lib/pgsql/14/data/pg_hba.conf`

`host all all ==server ip/32== md5`

zapisz i wyjdź z vima:

`:wq`

zrestartuj serwis:

`systemctl restart postgresql-14`

wejdź do postgresa i stwórz wszystkie bazy, które będą przywracane

`psql -U postgres -h ==ip_serwera==`

CREATE DATABASE ==nazwa_bazy== ;

stwórz role o takiej samej nazwie jak nazwa bazy:

`CREATE ROLE ==nazwa_roli==`

`WITH LOGIN PASSWORD '==hasło=='`

`INHERIT IN ROLE postgres;`

przypisz parametry dla roli:

`alter role ==nazwa_roli== set search_path = "$user", mplatform, ==nazwa_bazy== ;`

powtórz powyższe dla każdej bazy

wyjdź z postgresa

przejdź do lokalizacji, gdzie zapisane są pliki do przywrócenia i wgraj je do bazy

`psql -U postgres -h  server_ip  ==nazwa_bazy== < ==db_plik.sql==`

np: psql -U postgres -h 10.55.1.97 backoffice < db_backoffice.sql

Znane problemy:

użytkownik nie może podłączyć się do bazy z błędem o portach:

sprawdzić czy port 5432 jest otwarty na serwerze:

`sudo lsof -i -P -n | grep LISTEN`

jak nie jest, to otworzyć

z poziomu klienta sprawdzić, czy serwer wpuszcza połączenie:

`nc -zv ==ip_serwera== 5432`

jak nie wpuszcza to sprawdzić czy użytkownik ma dobrze skonfigurowanego VPN'a