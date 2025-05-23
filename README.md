# UTS Jaringan Komputer 2  
## Konfigurasi DHCP Server, DNS Server, dan Firewall (iptables)  
**Universitas Teknologi Bandung**  
Departemen Teknik Informatika — Kelas TIF K 23B  
Dosen: Muchamad Rusdan, S.T., M.T.  
Mahasiswa: Lita Alentina - 23552011097 

---

## Deskripsi  
Repositori ini berisi konfigurasi lengkap untuk tugas Ujian Tengah Semester (UTS) Jaringan Komputer 2, mencakup:  
- Instalasi dan konfigurasi DHCP Server menggunakan `isc-dhcp-server`  
- Instalasi dan konfigurasi DNS Server menggunakan `bind9`  
- Konfigurasi firewall menggunakan `iptables`  

Semua konfigurasi diuji pada Ubuntu Server yang dijalankan di VirtualBox/VMware/WSL.

---

## Struktur File  

| File                 | Keterangan                                  |
|----------------------|---------------------------------------------|
| `dhcpd.conf`         | Konfigurasi DHCP Server                      |
| `named.conf.local`   | Konfigurasi zona DNS lokal (forward & reverse)|
| `named.conf.options` | Pengaturan opsi DNS seperti forwarders      |
| `db.server.local`    | File zona forward DNS untuk domain server.local|
| `db.100`             | File zona reverse DNS untuk subnet 192.168.100.0/24|
| `firewall.rules`     | Script konfigurasi firewall (iptables)      |

---

## Cara Penggunaan  

1. **DHCP Server**  
   - Salin file `dhcpd.conf` ke `/etc/dhcp/`  
   - Restart service DHCP:  
     ```bash
     sudo systemctl restart isc-dhcp-server
     ```

2. **DNS Server**  
   - Salin file `named.conf.local` dan `named.conf.options` ke `/etc/bind/`  
   - Salin file `db.server.local` dan `db.100` ke `/etc/bind/`  
   - Restart service DNS:  
     ```bash
     sudo systemctl restart bind9
     ```

3. **Firewall (iptables)**  
   - Terapkan aturan firewall dengan:  
     ```bash
     sudo iptables-restore < firewall.rules
     ```

---

## Uji Coba  
- Cek IP otomatis di client dengan `ip a` atau `ifconfig`  
- Cek resolusi DNS dengan `ping server.local`, `nslookup server.local`, atau `dig server.local`  
- Cek aturan firewall dengan `sudo iptables -L -v` dan uji coba juga layanan berikut pada Client :
`ssh user@192.168.100.1`,
`curl http://192.168.100.1`,
`curl -k https://192.168.100.1`,
`ping 192.168.100.1`

---

## Tautan  
- [Video Dokumentasi dan Presentasi](https://youtu.be/2InAMcMxNug?si=joTvwazZQqCXnI-y)  
- [Repositori GitHub](https://github.com/LitaAlentina287/UTS_DHCP-DNS-Firewall_by-Lita.git)  
