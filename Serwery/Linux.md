# Mapa
- [Netplan](#netplan)
- [Samba](#samba)
- [Iptables](#iptables)
- [Crontab ?](#crontab-)
- [SSH](#ssh)
- [DHCP](#dhcp)
- [Apache](#apache)
- [DNS](#dns)
- [FTP](#ftp)
- [Quota](#quota)
- [Mail](#mail)
- [Polecenia](#polecenia)

# WAŻNE
**Rób backupy plików, PODCZAS EGZAMINU NIE BEDZIESZ MOG REINSTALLOWAĆ.**

# Netplan
Mam nadzieję, że nie będzie niczego oprócz konfiguracji karty.

```
sudo netplan apply
```
```
sudo netplan get all
```

---

### Plik konfiguracyjny `/etc/netplan/*.yaml` (można zrobić swój od 0)
![netplan](https://github.com/user-attachments/assets/d72cdcd0-ca44-4da8-b6fc-a1eb55ab7c72)

# Samba
Zrób backup przed i czytaj komentarze.

- Sprawdzanie konfiguracji
```
testparm
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

---

### Plik konfiguracyjny `/etc/samba/smb.conf`
![samba](https://github.com/user-attachments/assets/e235f7e7-0501-4da2-88aa-125fa4828a4c)

# Iptables

# Crontab ?

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

# Quota

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

