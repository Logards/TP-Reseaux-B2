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

Déterminer...

- à quelle adresse IP correspond le nom de domaine `www.ynov.com`

> Ca s'appelle faire un "lookup DNS".

- à quel nom de domaine correspond l'IP `174.43.238.89`

> Ca s'appelle faire un "reverse lookup DNS".

---

☀️ **Hop hop hop**

Déterminer...

- par combien de machines vos paquets passent quand vous essayez de joindre `www.ynov.com`

---

☀️ **IP publique**

Déterminer...

- l'adresse IP publique de la passerelle du réseau (le routeur d'YNOV donc si vous êtes dans les locaux d'YNOV quand vous faites le TP)

---

☀️ **Scan réseau**

Déterminer...

- combien il y a de machines dans le LAN auquel vous êtes connectés

> Allez-y mollo, on va vite flood le réseau sinon. :)

![Stop it](./img/stop.png)

# III. Le requin

Faites chauffer Wireshark. Pour chaque point, je veux que vous me livrez une capture Wireshark, format `.pcap` donc.

Faites *clean* 🧹, vous êtes des grands now :

- livrez moi des captures réseau avec uniquement ce que je demande et pas 40000 autres paquets autour
  - vous pouvez sélectionner seulement certains paquets quand vous enregistrez la capture dans Wireshark
- stockez les fichiers `.pcap` dans le dépôt git et côté rendu Markdown, vous me faites un lien vers le fichier, c'est cette syntaxe :

```markdown
[Lien vers capture ARP](./captures/arp.pcap)
```

---

☀️ **Capture ARP**

- 📁 fichier `arp.pcap`
- capturez un échange ARP entre votre PC et la passerelle du réseau

> Si vous utilisez un filtre Wireshark pour mieux voir ce trafic, précisez-le moi dans le compte-rendu.

---

☀️ **Capture DNS**

- 📁 fichier `dns.pcap`
- capturez une requête DNS vers le domaine de votre choix et la réponse
- vous effectuerez la requête DNS en ligne de commande

> Si vous utilisez un filtre Wireshark pour mieux voir ce trafic, précisez-le moi dans le compte-rendu.

---

☀️ **Capture TCP**

- 📁 fichier `tcp.pcap`
- effectuez une connexion qui sollicite le protocole TCP
- je veux voir dans la capture :
  - un 3-way handshake
  - un peu de trafic
  - la fin de la connexion TCP

> Si vous utilisez un filtre Wireshark pour mieux voir ce trafic, précisez-le moi dans le compte-rendu.

---

![Packet sniffer](img/wireshark.jpg)

> *Je sais que je vous l'ai déjà servi l'an dernier lui, mais j'aime trop ce meme hihi 🐈*