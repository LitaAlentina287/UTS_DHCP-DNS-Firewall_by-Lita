
UTS Jaringan Komputer 2 – DHCP, DNS, Firewall
Nama: Lita Alentina
NIM: 23552011097
Kelas: TIF K 23 CNS
Dosen Pengampu: Muchamad Rusdan, S.T., M.T.
Universitas Teknologi Bandung

Deskripsi Praktikum
Tujuan dari praktikum ini adalah mempelajari instalasi dan konfigurasi layanan DHCP, DNS, dan Firewall menggunakan Ubuntu Server 18.04. Sistem ini dibangun di atas simulasi dua mesin virtual (VM) dalam jaringan LAN internal menggunakan VirtualBox.

Topologi Virtual
[VM Server - Ubuntu Server 18.04]
  ├─ eth0 (NAT)
  └─ eth1 (Internal Network: 192.168.10.1)
         │
         └── [VM Client - Ubuntu Server/Desktop]
               └─ eth1 (DHCP Client)

Instalasi Ubuntu Server & Client di VirtualBox

VM Server
- Nama: Ubuntu-Server
- OS: Ubuntu Server 18.04 (ISO: ubuntu-18.04-live-server-amd64.iso)
- RAM: 1024 MB
- Disk: 10 GB
- Adapter 1: NAT
- Adapter 2: Internal Network (intnet)

VM Client
- Nama: Ubuntu-Client
- OS: Ubuntu Server/Desktop 18.04
- RAM: 1024 MB
- Disk: 10 GB
- Adapter 1: NAT (opsional)
- Adapter 2: Internal Network (intnet)

Konfigurasi DHCP Server

File: /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses: [192.168.10.1/24]

Perintah:
sudo netplan apply

Install DHCP Server:
sudo apt update
sudo apt install isc-dhcp-server

Konfigurasi Interface DHCP:
File: /etc/default/isc-dhcp-server
INTERFACESv4="enp0s8"

File Konfigurasi DHCP: /etc/dhcp/dhcpd.conf
authoritative;
default-lease-time 600;
max-lease-time 7200;
subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.100 192.168.10.200;
  option routers 192.168.10.1;
  option subnet-mask 255.255.255.0;
  option domain-name-servers 8.8.8.8;
  option domain-name "server.local";
}

Restart DHCP Server:
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server

Konfigurasi VM Client (Sebagai DHCP Client)

File: /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: true

Perintah:
sudo netplan apply

Verifikasi IP:
ip a  # Cek apakah mendapat IP dari DHCP Server (misal 192.168.10.101)

Tes Koneksi ke Server:
ping 192.168.10.1

File Konfigurasi yang Diunggah:
- /etc/dhcp/dhcpd.conf
- /etc/default/isc-dhcp-server
- /etc/netplan/01-netcfg.yaml

Catatan:
- Server menggunakan IP statis 192.168.10.1
- Client berhasil mendapatkan IP dari DHCP (otomatis)
- Selanjutnya konfigurasi DNS dan Firewall akan ditambahkan

Tautan Penting:
- YouTube Video: Akan diisi setelah diunggah
- GitHub Repository: https://github.com/namakamu/uts-jarkom-dhcp-dns-firewall
