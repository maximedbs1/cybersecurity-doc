# Fonctions de hachage

**SHA** (Secure Hash Algorithms) : Famille de fonctions de hachage publiées par le NIST comme standard FIPS. Comprend :
- **SHA-0**, publié en 1993, version originelle du hash 160 bit (taille de l’output), a été retiré rapidement après sa publication à cause d’une faiblesse significative dans l’algorithme
- **SHA-1**, publié en 1995, correction de SHA-0, designé par la NSA, des faiblesses cryptographiques ont été découvertes, le standard n’est plus indiqué pour la plupart des utilisations cryptographiques après 2010
- **SHA-2**, publiés en 2001, regroupant SHA-256 (mots de 32 bits) et SHA-512 (mots de 64 bits), il existe plusieurs version tronquées de ces 2 standards, également desginé par la NSA
- **SHA-3**, publié en 2015, supporte les mêmes longueurs que SHA-2 mais avec une structure interne très différente du reste des algo SHA.

**MD5** (Message Digest 5) : Fonction de hachage publiée en 1992. Output de 128 bits. Non recommandée aujourd’hui car peu résistants aux collisions, comme l’ont prouvé des recherches menées en 1996 et en 2004 sur la recherche de collisions qui ont prouvé la faiblesse du MD5. Encore utilisé seulement pour vérifier l’intégrité d’un fichier.