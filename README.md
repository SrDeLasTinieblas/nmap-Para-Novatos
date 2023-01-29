# nmap-Para-Novatos
 
 
 ## Fase 1: Recopilacion de informacion
  - Lo primero que se necesita es el target puedes pasar nombres de host, direcciones IP, redes, etc.
  - Los segundo hacemos un ping para confirmar que estoy en la red
 
 Ejemplo: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
1. Descrubir host en la red.
  - -sn: Ping Scan - disable port scan
 
`Escanemos todo los host de la red`
```
nmap -sn 192.168.56.0/24
```

`Como respuesta nos llega los host que tiene la red activos `
```
┌──(kali㉿kali)-[~]
└─$ nmap -sn 192.168.56.0/24 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-29 17:11 EST
Nmap scan report for 192.168.56.1
Host is up (0.00094s latency).
Nmap scan report for 192.168.56.102
Host is up (0.0041s latency).
Nmap scan report for 192.168.56.103
Host is up (0.0013s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 23.46 seconds
```

¿Como Saber si un equipo esta en la red? \
Agarro un host que esta activa y le hacemos un nmap -sn
```
nmap -sn 192.168.56.102
```

2. Enumerar servicios de esucha.
- En este paso detectaremos los puertos que estan activos enumerando los puertos
   
 - Cuando queremos scanear con el protocolo sincronismo TCP (si tiene firewall no funcionara)
 -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
```
sudo nmap -sS 192.168.56.102 
```
 - Filtramos por puerto
```
sudo nmap -sS 192.168.56.102 -p 80
```

`Como respuesta nos da el puerto activo y que servicio es `
```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sS 192.168.56.102 -p 80
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-29 17:43 EST
Nmap scan report for 192.168.56.102
Host is up (0.00086s latency).

PORT   STATE SERVICE
80/tcp open  http
MAC Address: 08:00:27:42:51:79 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 13.24 seconds
```
 - Ahora enumeraremos los servicios

 ```sudo nmap -sV 192.168.56.102 ```
 
 `Nos saldra los puerto, los estado, los servicios y las versiones`

 ```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sV 192.168.56.102   
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-29 18:01 EST
Nmap scan report for 192.168.56.102
Host is up (0.0012s latency).
Not shown: 991 filtered tcp ports (no-response)
PORT     STATE  SERVICE     VERSION
21/tcp   open   ftp         ProFTPD 1.3.5
22/tcp   open   ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
80/tcp   open   http        Apache httpd 2.4.7 ((Ubuntu))
445/tcp  open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
631/tcp  open   ipp         CUPS 1.7
3000/tcp closed ppp
3306/tcp open   mysql       MySQL (unauthorized)
8080/tcp open   http        Jetty 8.1.7.v20120910
8181/tcp closed intermapper
MAC Address: 08:00:27:42:51:79 (Oracle VirtualBox virtual NIC)
Service Info: Host: UBUNTU; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.57 seconds
 ```


