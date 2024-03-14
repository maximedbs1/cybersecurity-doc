# Protocoles de sécurité

**Kerberos** : Créé au MIT, Protocole d’authentification réseau reposant sur un mécanisme à chiffrement symétrique et l’utilisation de tickets (pas de mots de passes en clair pouvant être interceptés). Dialogue sur 88/udp par défaut. Utilisé massivement, notamment par les services Microsoft, il est applicable dans de nombreux procédés d’authentification dont le SSO.

Fonctionnement :
- Le client C a une clé secrète Kc
- Le serveur S a une clé secrète Ks
- Le TGS (Ticket Granting Service) a une clé secrète Ktgs et connaît Ks
- Le KDC (Key Distribution Center) connaît Kc et Ktgs

![Fonctionnement de Kerberos](/Resources/Images/Kerberoswork.png "Kerberoswork")

Le client C veut accéder à un service proposé par le serveur S

1. C s’authentifie auprès du KDC et lui indique le TGS qui l’intéresse ;
2. Après vérification d’identité, le KDC envoie une clé de session Kc,tgs (pour les communications entre C et TGS) chiffrée par Kc ainsi qu’un ticket Ttgs à C, chiffré par Ktgs ;
Le client possède alors un ticket Ttgs (qu’il ne peut pas déchiffrer) et une clé Kc,tgs
3. C envoie à TGS son ticket Ttgs ainsi que son identifiant + timestamp chiffré par Kc,tgs ;
4. Le TGS déchiffre le ticket avec sa clé Ktgs, récupère le contenu (dont la clé de session Kc,tgs) et peut déchiffrer l’identifiant de C et authentifier les requêtes ;
5. Le TGS envoie au client un ticket Ts chiffré par Ks et une clé de session Kc,s chiffrée avec Kc,tgs, pour les communications entre C et S ;
6. C envoie à S son ticket Ts et son identifiant chiffré par Kc,s ;
7. S vérifie la validité du ticket (le déchiffre avec sa clé Ks) et peut autoriser l’accès au service.

Le ticket Ttgs détenu par C lui sert de carte d’identité éphérmère (généralement 8 heures de validité) mais si nécessaire, un ticket peut être annulé prématurément.

[OC - Mouvement latéral avec le protocole Kerberos](https://openclassrooms.com/fr/courses/7723396-assurez-la-securite-de-votre-active-directory-et-de-vos-domaines-windows/7953376-effectuez-un-mouvement-lateral-avec-le-protocole-kerberos)

**LDAP** (Lightweight Directory Access Protocol) : Protocole réseau de communication avec annuaire pour des requêtes, recherches, modifications et autorisations rapides. Les informations y sont stockées sous forme d’une structure arborescente dont les nœuds sont constitués d’attributs associés à des valeurs. Port de transfert non sécurisé 389/tcp-udp, transfert chiffré 636/tcp-udp (LDAPS). Fonctions de structuration d’annuaires, ajout, modification et lecture de données, services d’authentification (via user/passwd, certificats ou jeton Kerberos), recherche sur les données prises en charge. Convient aux applications à très grande échelle pour traiter des millions de demandes. Très utilisé dans AD.

**NTLM** (New Technology LAN Manager) : (Considéré comme obsolète depuis 2010, remplacé par Kerberos) Protocole d’authentification qui était utilisé dans diverses implémentations des protocoles réseau Microsoft comme mécanisme SSO. Mécanisme de stimulation/réponse où le client prouve son identité sans envoyer de mot de passe au serveur.

**TLS** (Transport Layer Security) : Protocole de sécurisation des échanges réseau (couche transport). Successeur de SSL qui est maintenant obsolète. Chiffrement symétrique des flux de données (AES), la clé symétrique étant partagée via un échange asymétrique entre client et serveur (certificat X.509). Utilisé par des protocoles (SMTPS, FTPS…) et des applications (OpenSSL pour HTTPS notamment).

**SSL** (Secure Sockets Layer) : Protocole de sécurisation des échanges réseau aujourd’hui obsolète et remplacé par TLS.

**Ipsec** (Internet Protocol Security) : Protocole de protection des communications privées sur réseaux IP. Permet de crypter, décrypter, signer et vérifier les données. 2 modes de fonctionnement, mode transport (SSH-like) pour cryptage des données du paquet ainsi que hash pour l’intégrité. Mode tunnel (utilisation VPN) pour cryptage de tout le paquet, hash et encapsulation dans un nouveau paquet IP avec nouvelle en-tête (cache l’expéditeur et le destinataire, affiche seulement les IP des routeurs). Combine 3 protocoles, AH (Authentication Header) (51/tcp) pour la signature et donc authentification des paquets. ESP (Encapsulating Security Payload) (50/tcp) pour le chiffrement du paquet et l’ajout d’une nouvelle en-tête en mode tunnel. IKE (Internet Key Exchange) (500/udp) pour l’authentification des 2 routeurs, via certificats ou clé partagée, puis ouverture du tunnel.

**3-D Secure** : Protocole sécurisé de paiement sur internet. Développé par Visa et MasterCard en 1999. Echange de messages XML via connexions SSL pour chiffrement des requêtes et authentification client et serveur via certificats numériques. Lie l’autorisation financière avec l’authentification en ligne. Comporte 3 domaines (3-D) : 1. le commerçant et la banque qui recevra les fonds, 2. la banque qui a délivré la carte de paiement, 3. le système de carte bancaire. Se traduit généralement par la double authentification via SMS.

**SET** (Secure Electronic Transaction) : Protocole de sécurisation des transactions de paiement utilisant la carte bancaire développé en 1996. Élaboré conjointement par Visa, MasterCard et autres acteurs majeurs. Implique 3 parties : client, vendeur et banque du vendeur. Demande des certificats (X.509) aux 3 parties, ceux du client et du vendeurs sont fournis par leurs banques. Le numéro de carte n’est pas connu du vendeur donc pas de stockage. Assure la confidentialité avec DES, l’intégrité avec RSA + SHA-1 et l’authentification (certificats + autorité). Peu adopté sur le marché pour cause de complexité du protocole + logistique de distribution de certificats etc. Plus opérationnel depuis 2000, remplacé par 3-D Secure.

[SET - Wikipédia](https://fr.wikipedia.org/wiki/Secure_Electronic_Transaction)

**SSH (Secure Shell)**