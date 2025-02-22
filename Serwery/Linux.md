# Mapa
- [Netplan](#netplan)
- [Samba](#samba)
- [Crontab ?](#crontab-)
- [SSH](#ssh)
- [DHCP](#dhcp)
- [Apache](#apache)
- [DNS](#dns)
- [FTP](#ftp)
- [Quota](#quota)
- [Mail](#mail)

# WAŻNE
Rób backupy plików, PODCZAS EGZAMINU NIE BEDZIESZ MOG REINSTALLOWAĆ.

## Netplan
Mam nadzieję, że nie będzie niczego oprócz konfiguracji karty.

```
$ sudo netplan apply

$ sudo netplan get all
```

### Konfiguracja /etc/netplan/*.yaml (można zrobić swój od 0)
![netplan](https://github.com/user-attachments/assets/d72cdcd0-ca44-4da8-b6fc-a1eb55ab7c72)

## Samba
Zrób backup przed i czytaj komentarze.

- Sprawdzanie konfiguracji
```
$ testparm
```

- Utworzenia konta w sambie
```
pdbedit -a -y *user*
```

- Sprawdzanie użytkowników samby
```
pdbedit -L
```

- Sprawdzenie aktywnych zasobów
```
smbclient -L localhost
```

Aby anonimowo zmienić uprawnienia katalogu zasobu i katalogu domowego użytkownika.
Podczas testowania nie udało się otworzyć zasobu anonimowego na Windows 10 bez byle jakiego loginu.

### Plik konfiguracyjny /etc/samba/smb.conf
![samba](https://github.com/user-attachments/assets/e235f7e7-0501-4da2-88aa-125fa4828a4c)

## Crontab ?

## SSH

## DHCP

## Apache

## DNS

## FTP

## Quota

## Mail
