# Attaques en cryptographie

**Attaque des anniversaires** : Attaque sur des fonctions de hachage, basée sur des notions mathématiques similaires à celles du paradoxe des anniversaires en théorie des probabilités (ex : proba que sur une classe de 30 élèves, 2 d’entre eux aient la même date d’anniversaire (collision), est d’environ 0,70). Le but est de comparer un grand nombre de hash entre eux pour en trouver 2 similaires pour 2 sources différentes, appelé collision. Attaque utilisée pour modifier les communications entre 2 personnes ou encore faire signer de faux documents (prendre un contrat m et un contrat frauduleux m’, on va générer un grand nombre de variations de m et m’ en ajoutant des virgules, double espaces, synonymes, etc. On effectue un hash de toutes ces version jusqu’a trouver un hash similaire pour une version de m et une de m’, de là on peut faire signer le contrat frauduleux m’ au lieu de m). 

Approximation rapide du nombre n de hash nécessaires pour trouver une collision : n ≃ sqrt(2m * p(n)) 

ex : algo qui génère des hash de 32 bits (m=2^32) et on veut une proba de collision de 1/1.000.000 (p≃2^20) on a n≃sqrt(2x2^32x2^-20) ≃ 90,5 hash nécessaires (la réponse exacte est 93).

[(Explications détaillées)](https://fr.wikipedia.org/wiki/Attaque_des_anniversaires)