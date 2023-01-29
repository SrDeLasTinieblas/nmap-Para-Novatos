# nmap-Para-Novatos
 
 
 ## Fase 1: Recopilacion de informacion
 Lo primero que se necesita es el target puedes pasar nombres de host, direcciones IP, redes, etc.
 
 Ejemplo: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
1. Descrubir host en la red
     - -sn: Ping Scan - disable port scan
 
`Escanemos todo los host de toda la red`
```
nmap -sn 192.168.56.0/24
```
