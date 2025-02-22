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


## Polecenia
#### Systemowe
- dmidecode
- lsblk
- ...
#### Użytkownicy
- chown
- chmod -G
- ...
#### Uprawnienia
- chmod
- ...
  
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

## Podstawy Repozytoriów

## Konfiguracja GRUB 
