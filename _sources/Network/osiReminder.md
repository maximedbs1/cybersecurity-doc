# Rappels OSI

## Couches

|   | Type | N° | Nom | Fonctione |
|---|---|---|---|---|
| Couches Hautes  | Donnée | 7 | Application  | Point d’accès aux services réseau (HTTP/HTTPS) |
|                 | Donnée | 6 | Présentation | Gère le chiffrement et le déchiffrement des données, convertit les données machine en données explopitables par n’importe quelle autre machine (HTML/XML) |
|                 | Donnée | 5 | Session | Communication interhost, gère les sessions entre les différentes applications (Cookies) |
|                 | Segment / Datagramme | 4 | Transport | Connexion de bout en bout, connectabilité et contrôle de flux ; notion de port (TCP/UDP) |
| Couches Matérielles  | Paquet | 3 | Réseau | Détermine le parcours des données et l’adressage logique (IP) |
|                 | Trame | 2 | Liaison | Adressage physique (Ethernet/Adresse MAC) |
|                 | Bit / Symbole | 1 | Physique | Transmission des signaux sous forme numérique ou analogique (RJ45, Câbles Cat.5, etc.) |

## Quelques protocoles associés

| N° | Nom | Protocoles |
|---|---|---|
| 7 | Application | DHCP – DNS – FTP – HTTP – LDAP – RDP – RPC – SMB – SNMP – SMTP – SSH – Telnet – BitTorrent – VoIP - Web |
| 6 | Présentation | ASCII – CSS – HTML – MIME – SSL – TLS – Unicode – XML - JSON |
| 5 | Session | NetBIOS – RPC - AppleTalk |
| 4 | Transport | TCP – UDP - SPX |
| 3 | Réseau | ARP – ICMP – IP – Ipv4 – Ipv6 |
| 2 | Liaison | Ethernet – PPP – ATM - CAN |
| 1 | Physique | ADSL – Bluetooth – USB – WiFi – Câble coaxial – Paire torsadée – ISDN
 |