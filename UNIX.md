**ALL**

*Kopiowanie z remotem*


To copy all from Local Location to Remote Location (Upload)

`scp -r /path/from/local username@hostname:/path/to/remote`
To copy all from Remote Location to Local Location (Download)

`scp -r username@hostname:/path/from/remote /path/to/local`
Custom Port where xxxx is custom port number

`scp -r -P xxxx username@hostname:/path/from/remote /path/to/local`
Copy on current directory from Remote to Local

`scp -r username@hostname:/path/from/remote`

*Random*

flush dnsow

`sudo systemd-resolve --flush-caches`


`systemctl restart NetworkManager`


`sudo lsof -i -P -n | grep LISTEN`


`sudo netstat -tulpn | grep LISTEN`


`sudo ss -tulpn | grep LISTEN`


`sudo lsof -i:22` see a specific port such as 22 

*Sprawdzic bo chyba przydatne*

!atrybuty

digg

chattr +i &lt;plik&gt; zmienia permission pliku, nie mozna go juz adytowach


The **nc** (or netcat) utility is used for just about anything under the sun

involving TCP, UDP, or UNIX-domain sockets. It can open TCP connections,

send UDP packets, listen on arbitrary TCP and UDP ports, do port scan‐

ning, and deal with both IPv4 and IPv6. Unlike telnet(1), nc scripts

nicely, and separates error messages onto standard error instead of send‐

ing them to standard output, as telnet(1) does with some.

**CENTOS**

 ustawienie sieci:

 `/etc/sysconfig/network-scripts/ifcfg-ens192`

**UBUNTU**

 ustawienie sieci:
 `/etc/resolv.conf'



