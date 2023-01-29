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
   - En este paso detectaremos los puertos que estan activos 
   
 - Cuando queremos scanear con el protocolo sincronismo TCP (si tiene firewall no funcionara)
 -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
```
sudo nmap -sS 192.168.56.102 
```
 - Filtramos por puerto
```
sudo nmap -sS 192.168.56.102 -p 80
```





