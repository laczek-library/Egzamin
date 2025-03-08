# Mapa
- [~Netplan~](#netplan)
- [~Samba~](#samba)
- [~Firewall~](#firewall-iptables-ufw)
- [Crontab](#crontab)
- [SSH](#ssh)
- [~DHCP~](#dhcp)
- [Apache](#apache)
- [DNS](#dns)
- [~FTP~](#ftp)
- [Quota](#quota)
- [Mail](#mail)
- [Polecenia](#polecenia)

# WAŻNE
**Rób backupy plików, PODCZAS EGZAMINU NIE BEDZIESZ MOG REINSTALLOWAĆ.**

**RÓB ĆWICZENIA LOGICZNIE, MOGĄ BYĆ LITERÓWKI W SCREENSHOTACH**

# Netplan
Mam nadzieję, że nie będzie niczego oprócz konfiguracji karty.

```sh
sudo netplan apply
```
```sh
sudo netplan get all
```

---

### Plik konfiguracyjny `/etc/netplan/*.yaml` (można zrobić swój od 0)
![netplan](https://github.com/user-attachments/assets/d72cdcd0-ca44-4da8-b6fc-a1eb55ab7c72)

# Samba
Zrób backup przed i czytaj komentarze.

- Sprawdzanie konfiguracji
```sh
testparm
```

- Utworzenia konta w sambie
```sh
pdbedit -a -y *user*
```

- Sprawdzanie użytkowników samby
```sh
pdbedit -L
```

- Sprawdzenie aktywnych zasobów
```sh
smbclient -L localhost
```

Aby anonimowo zmienić uprawnienia katalogu zasobu i katalogu domowego użytkownika.

Podczas testowania nie udało się otworzyć zasobu anonimowego na Windows 10 bez byle jakiego loginu.

---

### Plik konfiguracyjny `/etc/samba/smb.conf`
![samba](https://github.com/user-attachments/assets/e235f7e7-0501-4da2-88aa-125fa4828a4c)

# Firewall (iptables, ufw)
## UFW
- Status
```
sudo ufw status
```
- Uruchamianie
```
sudo ufw enable
```

```
sudo ufw disable
```
- Reset
```
sudo ufw reset
```
- Dodawanie zasad
```
sudo ufw allow 1000:2000/tcp

sudo ufw allow https
```
- Blokowanie
```
sudo ufw deny 550
```
- Usuwanie zasad
```
sudo ufw delete *numer zasady*
```
- Domyślne
```
sudo ufw default deny incoming 

sudo ufw default allow outgoing
```
## Iptables
- Opcje  
	`INPUT` - przychodzący  
	`OUTPUT` - wychodzący  
	`FORWARD` - ruch przekazywany  
	`DROP` - blokowanie  
	`ACCEPT` - przepuszczanie  
	`REJECT` - blokowanie i wysłanie odpowiedzi  
	` -P ` - ustawienie domyślnej zasady   
	` -A ` - (append) dodaj do tablicy  
	` -p ` - ustaw protokół  
	` -s ` - (source) źródło  
	` --dport ` - (destination port)   
	` -j ` - ustawia czy przepuszcza (`ACCEPT`) czy blokuje (`DROP`)  
- Listowanie zasad
```
sudo iptables -L
```
- Przepuszczanie
```
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
- Blokowanie
```
sudo iptables -A INPUT -s 10.9.8.5 -j DROP
```
- Resetowanie
```
sudo iptables -F
```
- Domyślne
```
sudo iptables -P INPUT DROP 

sudo iptables -P OUTPUT ACCEPT 

sudo iptables -P FORWARD DROP
```



# Crontab

# SSH

# DHCP
### **CZYTAJ KOMENTARZE**
### **NIE DODAŁEM JAK SIĘ ROBI NA IPV6 (przynajmniej na teraz)**

- Nazwa usługi  
`isc-dhcp-server`

- Karta DHCP  
`/etc/default/isc-dhcp-server`

    np.
    `INTERFACESv4="eno1"`

- Plik konfiguracyjny  
`/etc/dhcp/dhcpd.conf`

- Plik przykładowy  
`/usr/share/doc/isc-dhcp-server/examples/dhcpd.conf.example`

- Pobieranie ustawień na Windowsie i Ubuntu  
  - restart karty
  - ```sh
    dhclient  # nie jest zawsze pobrane
    ```

- Lista dzierżaw  
```sh
sudo dhcp-lease-list
```  

Mi nie działało, ale powinno.  

---

### Rezerwacja  
Wyskakuje kilka błędów (ale działa 👌):
- jak się da adres z range'a 
- małe ostrzeżenie jak z zadeklarowanego subnetu (nie wyczyściłem tablicy)
  
Nie działa jak dasz adres z poza ^

### Dla kilku podsieci użyj:
`shared-networks *nazwa sieci* {
...
}`

---

### Masquerade  
- W pliku `/etc/sysctl.conf` ustaw (odkomentuj) linijkę:  
`net.ipv4.ip_forward=1`  
```sh
sudo sysctl -p  # sprawdza co odkomentowałeś
```
- Dodanie reguły do iptables:  
```sh
sudo iptables -t nat -A POSTROUTING -s *adres sieci*/*maska* -j MASQUERADE
```

---

### Plik konfiguracyjny `/etc/dhcp/dhcpd.conf`
![dhcp](https://github.com/user-attachments/assets/e3c57c51-af5d-4430-80d5-94ebe14a7c4e)

# Apache

# DNS

### Plik konfiguracyjny `/etc/bind/*` (tymczasowy)
![dns](https://github.com/user-attachments/assets/50912651-9d5d-41aa-a291-5af244106313)


# FTP
### **CZYTAJ KOMENTARZE**
- Domyślny katalog konta ftp `/srv/ftp`
- Otwórz [firewall](#firewall-iptables-ufw)
- Żeby coś zapisać (putować) katalog musi miec 777 (moze 751 - mi nie działało)
- Przeglądarka plików Windowsa używa portów 40000:50000
    - otwórz je w firewallu
    - dodaj: `pasv_min_port=40000` i `pasv_max_port=50000`
- Istnieje `mput` i `mget`
- Zmiana trybu między binarnym i ascii najłatwiej w kliencie ftp
- Zmiana katalogu domowego użytkownika ftp
  
np.
```sh
sudo usermod -d *ścieżka* *użytkownik*
```
```sh
sudo usermod -d /ftp ftp
```

#### Sprawdzanie pliku konfiguracyjnego (USŁUGA MUSI BYĆA ZATRZYMANA i chyba muszż być domyślne porty - nie chciało mi się sprawdzać przy testowaniu)
```sh
sudo vsftpd /etc/vsftpd.conf
```
### Szyfrowane
- Dla TLS otworzyć port 990
- Testowanie połączenia szyfrowanego
```sh
lftp localhost -d -u *uzytkownik*
```
### Potencjalne problemy
- Dla kilku rozszerzeń musi byc w {} i bez spacji po przecinku   
  `hide_file={*.txt,*.log}`

### **Wytłumaczenie: `chrootlist` - `userlist` - `ftpusers`** (nie testowałem, ale raczej dobrze)
- wszystkim plikom można ustawić swoją ścieżkę,
  domyślna ścieżka dla ftpusers to `/etc/ftpusers`
1. `chrootlist`
   - Lista użytkowników, którzy mają być uwięzieni w swoich katalogach domowych lub określonym katalogu.
   - `chroot_local_user=YES` -  wszyscy lokalni użytkownicy będą ograniczeni do swoich katalogów domowych
   - `chroot_list_enable=YES` - konta na liście będą uwięzione
   - `allow_writeable_chroot=YES` - pozwala na zapisywanie w uwięzionym katalogu (domyślnie nie można)
2. `userlist`
   - Lista użytkowników, którym zezwolono lub zabroniono dostępu/logowania w zależności od konfiguracji.
   - `userlist_enable=YES` - włącza działanie pliku `userlist`
   - `userlist_deny=NO` - pozwala **TYLKO** użytkownikom z listy na logowanie się.
   - `userlist_deny=YES` - użytkownicy będą odmówione dostępu do FTP
3. `ftpusers`
    - Kompletnie blokuje użytkowników od logowania się na serwer FTP.

### Plik konfiguracyjny `/etc/vsftpd.conf`
![vsftpd](https://github.com/user-attachments/assets/308c0b19-5824-446e-9887-53ff5a1add86)




# Quota
na logike

# Mail

# Polecenia
```sh
resolvectl        # DNS-y
tracert
dhclient          # Pobieranie ustawień DHCP
nmcli             # Ustawienia karty
```

- Dodanie tymczasowego adresu
```sh
sudo ip addr add *adres*/*maska* dev *karta*
```

