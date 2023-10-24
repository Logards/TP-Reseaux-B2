# TP1 : Maîtrise réseau du poste

# I. Basics

☀️ **Carte réseau WiFi**

```
[bastien@fedora ~]$ ip a | grep link/ether
    link/ether 6c:94:66:1f:be:8b

[bastien@fedora ~]$ ip a | grep 10.33.65.80/20
    inet 10.33.65.80/20
  
[bastien@fedora ~]$ ip a | grep 10.33.65.80/20
    inet 10.33.65.80/20 
```

---

☀️ **Déso pas déso**

```
Adresse de réseau : 10.33.64.0
Adresse de broadcast : 10.33.79.255
Nombre d'adresses IP disponibles : 4094
```

Calcul avec ça : https://cric.grenoble.cnrs.fr/Administrateurs/Outils/CalculMasque/
---

☀️ **Hostname**

```
[bastien@fedora ~]$ hostname
fedora
```
---

☀️ **Passerelle du réseau**

```
[bastien@fedora ~]$ ip neigh
10.33.79.254 dev wlo1 lladdr 7c:5a:1c:d3:d8:76 REACHABLE 
```
---

☀️ **Serveur DHCP et DNS**

```
[bastien@fedora ~]$ ip neigh
10.33.79.254

[bastien@fedora ~]$ cat /etc/resolv.conf | grep nameserver
nameserver 127.0.0.53
```
Le pc utilise son propre dns, il est le serveur dns mais il connait d'autre dns :
```
[bastien@fedora ~]$ resolvectl
Current DNS Server: 1.1.1.1
       DNS Servers: 8.8.8.8 1.1.1.1
```
---

☀️ **Table de routage**

```
[bastien@fedora ~]$ ip r s | head -n 1
default via 10.33.79.254 dev wlo1 proto dhcp src 10.33.65.80 metric 600 
```

---

![Not sure](./img/notsure.png)

# II. Go further

> Toujours tout en ligne de commande.

---

☀️ **Hosts ?**

```
[bastien@fedora ~]$ ping b2.hello.vous
PING b2.hello.vous (1.1.1.1) 56(84) octets de données.
64 octets de b2.hello.vous (1.1.1.1) : icmp_seq=1 ttl=57 temps=37.9 ms
^C
--- statistiques ping b2.hello.vous ---
1 paquets transmis, 1 reçus, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 37.897/37.897/37.897/0.000 ms
```

---

☀️ **Go mater une vidéo youtube et déterminer, pendant qu'elle tourne...**

[Les trames de la vidéo](./vidéo_dramaturgy.pcapng)

```
Ip address : 77.136.192.84
port : 51477
port pc : 443
```

---

☀️ **Requêtes DNS**

```
[bastien@fedora ~]$ host www.ynov.com
www.ynov.com has address 104.26.10.233
www.ynov.com has address 172.67.74.226
www.ynov.com has address 104.26.11.233
www.ynov.com has IPv6 address 2606:4700:20::ac43:4ae2
www.ynov.com has IPv6 address 2606:4700:20::681a:ae9
www.ynov.com has IPv6 address 2606:4700:20::681a:be9
```

```
[bastien@fedora ~]$ host 174.43.238.89
89.238.43.174.in-addr.arpa domain name pointer 89.sub-174-43-238.myvzw.com.
```

---

☀️ **Hop hop hop**

```
[bastien@fedora ~]$ traceroute www.ynov.com
traceroute to www.ynov.com (104.26.11.233), 30 hops max, 60 byte packets
 1  _gateway (10.33.79.254)  6.426 ms  6.382 ms  6.372 ms
 2  145.117.7.195.rev.sfr.net (195.7.117.145)  1.339 ms  1.326 ms  1.316 ms
 3  * * *
 4  196.224.65.86.rev.sfr.net (86.65.224.196)  3.650 ms  6.822 ms  3.630 ms
 5  68.150.6.194.rev.sfr.net (194.6.150.68)  35.630 ms  35.623 ms 12.148.6.194.rev.sfr.net (194.6.148.12)  11.148 ms
 6  12.148.6.194.rev.sfr.net (194.6.148.12)  11.931 ms 68.150.6.194.rev.sfr.net (194.6.150.68)  34.349 ms  34.339 ms
 7  141.101.67.48 (141.101.67.48)  9.866 ms  9.834 ms  10.495 ms
 8  141.101.67.54 (141.101.67.54)  13.148 ms 172.71.132.4 (172.71.132.4)  9.610 ms 172.71.120.4 (172.71.120.4)  10.667 ms
 9  104.26.11.233 (104.26.11.233)  9.603 ms  9.596 ms  9.589 ms
```

Passe par 9 machines.
---

☀️ **IP publique**

```
[bastien@fedora ~]$ curl ifconfig.me
195.7.117.146
```

---

☀️ **Scan réseau**

```
[bastien@fedora ~]$ sudo nmap -sn 10.33.71.104/20
Nmap done: 4096 IP addresses (859 hosts up) scanned in 510.69 seconds
```

# III. Le requin

---

☀️ **Capture ARP**

[Arp request](Arp_request.pcapng)


☀️ **Capture DNS**

```
[bastien@fedora ~]$ host crunchyroll.com
```

[Crunchyroll](DNS_Request_crunchyroll.pcapng)

---

☀️ **Capture TCP**

```
[Tcp try handshake](Tcp_Crunchyroll.pcapng)
```
---

![Packet sniffer](img/wireshark.jpg)

> *Je sais que je vous l'ai déjà servi l'an dernier lui, mais j'aime trop ce meme hihi 🐈*