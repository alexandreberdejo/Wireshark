# Network Sniffing — Wireshark

Projet réalisé à La Plateforme dans le cadre de la formation en administration et sécurité des infrastructures réseaux.

L'objectif est d'apprendre à capturer et analyser du trafic réseau avec Wireshark, de comprendre les protocoles courants, et de mettre en évidence les différences entre protocoles chiffrés et non chiffrés.

---

## Contenu du projet

**Partie 1 — VM Windows**

Mise en place d'une VM Windows 11 sous VMware Workstation Pro 17. Installation de Wireshark et premières captures sur interface NAT.

Protocoles analysés : TCP, ARP, UDP, SSDP

**Partie 2 — Réseau local Debian (client / serveur)**

Deux VM Debian 13 interconnectées. Installation de services réseau sur le serveur (FTP, Apache/HTTPS, DHCP, DNS, mDNS). Captures depuis le client.

Protocoles analysés : FTP, HTTPS/TLS, DHCP, DNS, mDNS

Observation clé : les identifiants FTP passent en clair sur le réseau, contrairement au trafic HTTPS qui reste illisible même avec accès complet à la capture.

**Partie 3 — Analyse en ligne de commande**

Utilisation de tshark pour automatiser les captures sans interface graphique. Filtres BPF et filtres d'affichage, redirection vers fichiers, sauvegarde au format PCAPNG.

---

## Stack technique

- Wireshark 4.6.5 (Windows), 4.4.15 (Debian)
- tshark (CLI)
- VMware Workstation Pro 17
- Windows 11, Debian 13
- vsftpd, Apache2, dnsmasq, avahi-daemon

---

## Commandes tshark essentielles

```bash
# Lister les interfaces
tshark -D

# Capturer avec filtre
tshark -i ens33 -f "udp port 53"

# Filtre d'affichage sur flag TCP
tshark -i ens33 -Y "tcp.flags.syn == 1 || tcp.flags.fin == 1"

# Sauvegarder et relire
tshark -i ens33 -w capture.pcapng
tshark -r capture.pcapng -Y "arp"
```

---

## Ce que ce projet m'a appris

- La différence concrète entre une trame (couche 2) et un paquet (couche 3)
- Comment lire un Three-Way Handshake TCP dans une capture réelle
- Pourquoi FTP est dangereux et HTTPS ne l'est pas, avec preuve à l'appui
- L'utilisation de tshark pour des captures scriptées et reproductibles
- Les bases de l'analyse de sécurité réseau : scan de ports, ARP spoofing, DNS tunneling

---

## Ressources

- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [RFC 793 — TCP](https://tools.ietf.org/html/rfc793)
- [RFC 826 — ARP](https://tools.ietf.org/html/rfc826)
- [RFC 1035 — DNS](https://tools.ietf.org/html/rfc1035)

---

Auteur : BERDEJO Alexandre — 2026
