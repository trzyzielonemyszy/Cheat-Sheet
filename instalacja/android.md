instalacja VM: Android

po zamontowaniu ISO:

*\- Installation- install Android-x86 to harddisc*

Partycja: *create/modyfy partitions*

*GPT: no*

utoworz partycje:

\[New\] --> \[primary\] --> \[bootable\] -->\[Write\] --> yes -->\[Quite\]

podświetl właśnie utworzoną partycje --> *ok*

wybierz *ext4* jako format plików i *yes* żeby sformatować

GRUB boot loader --> yes

system directory as read-write -->yes

reboot

odmontuj ISO

po reboocie pojawi sie shelll:

```
mkdir /data/fs
```

```
mount /dev/block/sda1 /data/fs
```

```
vi /data/fs/grub/menu.lst
```
w poniższej linii 
![quiet](uploads/80039005ddbcdbe0342bd39a26dfc80f/quiet.png)



zmień słowo 'quiet' na 'nomodeset xforcevesa'

zapisz i wyjdz
`:wq`
`reboot`

powinien właczyć sie android z GUI

siec :

wybierz *dodaj Nowa Siec*

SSID: VirtWifi

opcje zaawansowane:

ustawiaenia IP zmien z DHCP na statyczny:

ip : 10.55.1.xx

Brama:10.55.1.114

dlugość przedrostka sieci: 24

DNS1: 10.55.1.29

zapisz

dokoncz instalacje w sttandardowy sposób