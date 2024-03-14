# Protocoles de base

**NetBIOS** (Network Basic Input Output System) : Architecture réseau pour du transfert de fichier entre machines d’un LAN co-développé par IBM et Sytec vers 1985. Principalement utilisé par Microsoft. Pas un protocole réseau mais un système de nommage et une interface logicielle qui permet d’établir des sessions entre différents ordinateurs d’un réseau (une sorte de DNS mais qui fonctionne sur réseau local). 3 implémentations, la dernière, NBT (NetBIOS over TCP/IP), est la seule encore utilisée. Tend à disparaître car on utilise plus les noms DNS que les noms NetBIOS et le partage de fichiers avec SMB peut à présent se passer de NetBIOS et fonctionner directement au dessus de TCP/IP. Couche 5 (session) du modèle OSI. Utilise 4 ports : 135 Microsoft RPC service de localisation utilisé par les appels de procédure à distance, 137/udp NetBIOS Name Service pour associer un nom d’ordinateur à une adresse IP (nom limité à 15 caractères ASCII + 1 pour le type de machine), 138/udp NetBIOS Datagram Service pour échanger des messages en mode non connecté. 139/tcp NetBIOS Session Service pour échanger des messages en mode connecté.

![En-tête paquet Netbios](/Resources/Images/netbiosPacket.png "netbiosPacket")

[(NetBIOS — Wikipédia)](https://fr.wikipedia.org/wiki/NetBIOS)

[(Explication du fonctionnement général)](https://superuser.com/questions/637696/what-is-netbios-does-windows-need-its-ports-137-and-138-open#:~:text=A%20session%20management%20and%20data%20transport%20protocol%20NetBIOS,transfer.%205%20Protocol%20and%20adapter%20monitoring%20and%20management.)

**SMTP** (Simple Mail Transfer Protocol) : Protocole de communication utilisé pour transférer un courriel vers des serveurs de messagerie électronique. Dialogue sur 25/tcp sans chiffrement et 587/tcp en mode chiffré (TLS). Utilisable en mode CLI avec quelques commandes simples. Implémenté par tous les clients de messagerie en mode logiciel ou web.

**SMB** (Server Message Block) : Protocole de partage de ressources (systèmes de fichiers, répertoires et imprimantes) sur des réseaux locaux avec des machines Windows. Communique sur 445/tcp-udp avec Microsoft Directory Services (DNS), 139/tcp avec NetBIOS. Architecture client/serveur. Les anciennes versions sont toujours utilisées pour des raisons de compatibilité ce qui pose des problèmes de sécurité importants si mauvaise utilisation. Le logiciel libre Samba implémente le protocole SMB sur les systèmes UNIX.

**RPC** (Remote Procedure Call) : Protocle permettant de faire des appels de procédure sur des machines distantes en mode client/server. Communique sur 135/tcp-udp. Couche 5 (session) du modèle OSI. Concerne la communication entre les processus d’un système et les processus de machines distinctes. Utilisé dans les OS actuels pour réaliser des routines. Appliqué plus généralement dans les services web, les applications distribuées dans lesquelles différents ordinateurs partagent les ressources disponibles et les tâches, également dans le cloud computing, les réseaux peer-to-peer et la blockchain.

![Fonctionnement RPC](/Resources/Images/RPCwork.png "RPCwork")

[(Plus d'infos)](https://www.ionos.fr/digitalguide/serveur/know-how/quest-ce-que-le-remote-procedure-call/)

**RDP** (Remote Desktop Protocol) : Protocole principal pour les sessions de bureau à distance (employés qui ont accès à leur ordinateur de bureau depuis une autre machine par exemple). Port 3389/tcp-udp. 2 vulnérabilités principales : ces connexions à distances sont souvent ouvertes à des attaques brute-force ce qui est utile si le mdp est assez faible (utilisateur et/ou entreprise négligeants), accès non restreint au port utilisé par RDP (3389 généralement) qui peut donc être ciblé facilement (on-path attack).

**WinRM** (Windows Remote Management)

**ATM**

**ZigBee**

**ISDN**

**RIP** (Routing Information Protocol)

**SIP** (Session Initiation Protocol)

**IGMP** (Internet Group Management Protocol)