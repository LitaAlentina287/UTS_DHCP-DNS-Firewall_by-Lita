# UTS Jaringan Komputer 2  
## Konfigurasi DHCP Server, DNS Server, dan Firewall (iptables)  
**Universitas Teknologi Bandung**  
Departemen Teknik Informatika — Kelas TIF K 23B  
Dosen: Muchamad Rusdan, S.T., M.T.  
Mahasiswa: [Lita Alentina] (23552011097)  

---

## Deskripsi  
Repositori ini berisi konfigurasi lengkap untuk tugas Ujian Tengah Semester (UTS) Jaringan Komputer 2, mencakup:  
- Instalasi dan konfigurasi DHCP Server menggunakan `isc-dhcp-server`  
- Instalasi dan konfigurasi DNS Server menggunakan `bind9`  
- Konfigurasi firewall menggunakan `iptables`  

Semua konfigurasi diuji pada Ubuntu Server yang dijalankan di VirtualBox/VMware/WSL.

---

## Struktur File  

| File                         | Keterangan                                    |
|------------------------------|-----------------------------------------------|
| `/etc/dhcp/dhcpd.conf`        | Konfigurasi DHCP Server                        |
| `/etc/bind/named.conf.local`  | Konfigurasi zona DNS lokal (forward & reverse)|
| `/etc/bind/db.server.local`   | File zona forward DNS untuk domain server.local|
| `/etc/bind/db.100`            | File zona reverse DNS untuk subnet 192.168.100.0/24|
| `iptables.rules`              | Script konfigurasi firewall (iptables)        |

---

## Cara Penggunaan  

1. **DHCP Server**  
   - Instal `isc-dhcp-server`  
   - Salin file `dhcpd.conf` ke `/etc/dhcp/`  
   - Restart service DHCP:  
     ```bash
     sudo systemctl restart isc-dhcp-server
     ```

2. **DNS Server**  
   - Instal `bind9`  
   - Salin file konfigurasi ke `/etc/bind/`  
   - Pastikan `named.conf.local` memuat konfigurasi zona  
   - Restart service DNS:  
     ```bash
     sudo systemctl restart bind9
     ```

3. **Firewall (iptables)**  
   - Terapkan aturan firewall dengan:  
     ```bash
     sudo iptables-restore < iptables.rules
     ```

---

## Uji Coba  
- Cek IP otomatis di client dengan `ip a` atau `ifconfig`  
- Cek resolusi DNS dengan `ping server.local`, `nslookup server.local`, atau `dig server.local`  
- Cek aturan firewall dengan `sudo iptables -L -v`

---

## Tautan  
- [Video Dokumentasi dan Presentasi] (https://youtu.be/2InAMcMxNug?si=joTvwazZQqCXnI-y)
- [Repositori GitHub](https://github.com/LitaAlentina287/UTS_DHCP-DNS-Firewall_by-Lita.git)  

---

