Ubuntu Desktop

# MAPA
- [Polecenia](#polecenia)
  - [Systemowe](#systemowe)
  - [Użytkownicy](#użytkownicy)
  - [Uprawnienia](#uprawnienia)
- [Archiwizacja Danych](#archiwizacja-danych)
- [Budowa Środowiska Graficznego (DE) + Struktura Plików](#budowa-środowiska-graficznego-de--struktura-plików)
- [Podstawy Repozytoriów](#podstawy-repozytoriów)
- [Konfiguracja GRUB ](#konfiguracja-grub)


## Archiwizacja Danych
#### Rozszerzenia:
- .tar
- .tar.gz
- .tar.bz2

#### Zapakowanie pliku
```
tar -cvf *plik zarchiwizowany.tar* *plik do archiwizacji*
```
#### Odpakowanie pliku 
```
tar -xvf *plik zarchiwizowany.tar* /-C *katalog do którego odpakować*
```
np.
```
tar -cvf n_sbin.tar ~/Lista.txt
tar -xvf n_sbin.tar
tar -xvf n_sbin.tar -C ~
```

## Budowa Środowiska Graficznego (DE) + Struktura Plików
Aha

```sh
startx
```

## Podstawy Repozytoriów
- DPKG
- APT

```sh
sudo add-apt-repository *nazwa_repozytoria*
```

## Konfiguracja GRUB
/etc/grub.d

/etc/default/grub

/boot/grub/

```sh
sudo update-grub
```

## Polecenia
#### Systemowe
```sh
dmidecode     # hardware info
uname         # system info
lsblk         # list block devices
du            # disk usage
df            # disk space usage
top           
ps            # process status
fdisk         
mnt           
hwinfo        
lshw          # list hardware
hostnamectl   
history       
ln            # links
```
#### Użytkownicy
```sh 
userdel      
useradd      
adduser      # script
usermod
usermod -G   
```
#### Uprawnienia
```sh
chmod   
chown 
mv           # rename 
```
