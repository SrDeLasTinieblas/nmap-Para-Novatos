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

`Como respuesta nos da el puerto activo y que servicio es: `
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

 ```
 sudo nmap -sV 192.168.56.102 
 ```
 
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

`De esta manera podemos ver la version del SO.`

``` 
sudo nmap -v -O 192.168.56.102
```

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -v -O 192.168.56.102
[sudo] password for kali: 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-29 18:26 EST
Initiating ARP Ping Scan at 18:26
Scanning 192.168.56.102 [1 port]
Completed ARP Ping Scan at 18:26, 0.12s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 18:26
Stats: 0:00:02 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
Parallel DNS resolution of 1 host. Timing: About 0.00% done
Completed Parallel DNS resolution of 1 host. at 18:26, 13.01s elapsed
Initiating SYN Stealth Scan at 18:26
Scanning 192.168.56.102 [1000 ports]
Discovered open port 21/tcp on 192.168.56.102
Discovered open port 22/tcp on 192.168.56.102
Discovered open port 80/tcp on 192.168.56.102
Discovered open port 8080/tcp on 192.168.56.102
Discovered open port 445/tcp on 192.168.56.102
Discovered open port 3306/tcp on 192.168.56.102
Discovered open port 631/tcp on 192.168.56.102
Completed SYN Stealth Scan at 18:26, 5.05s elapsed (1000 total ports)
Initiating OS detection (try #1) against 192.168.56.102
Nmap scan report for 192.168.56.102
Host is up (0.0018s latency).
Not shown: 991 filtered tcp ports (no-response)
PORT     STATE  SERVICE
21/tcp   open   ftp
22/tcp   open   ssh
80/tcp   open   http
445/tcp  open   microsoft-ds
631/tcp  open   ipp
3000/tcp closed ppp
3306/tcp open   mysql
8080/tcp open   http-proxy
8181/tcp closed intermapper
MAC Address: 08:00:27:42:51:79 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Uptime guess: 199.639 days (since Thu Jul 14 04:06:38 2022)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: All zeros

Read data files from: /usr/bin/../share/nmap
OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.80 seconds
           Raw packets sent: 2018 (90.438KB) | Rcvd: 24 (1.354KB)
```                                                                             

3. Descrubir superficies de ataques vulnerables.

```
sudo nmap -v -sS --script=vuln 192.168.56.102 
```


4. Documentar la vulneravilidad.
 - -v : Le estamos diciendo que haga un analisis mas a detalle y muestre mayor informacion.
 - --reason : Es para explicar la razon del por que esta abierto o cerrado un puerto.
 - -oX : Es para que todo se exporte en el archivo Fase1.xml.
 - --stylesheet : Aqui le decimos que queremos adaptar todo a una hoja de estilos.
 - <IP> : Este es para decirle que maquina tenemos de target

```
 sudo nmap -v -sS --reason -oX Fase1.xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" 10.0.2.15
 ```

`Esto es para darle todos los permisos al archivo Fase1.xml`
 
```
 chmod 777 Fase1.xml 
 ```




