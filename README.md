# INFO-001_maziere_luque

> Xavier Mazière  
> Mattéo Luque

## Q1

### Chiffrement RSA

Pour chiffrer un message M en utilisant RSA, on effectue le calcul suivant :

`C = M^e mod n`

Où :

- M est le message en clair (converti en valeur numérique)
- C est le message chiffré
- e est l'exposant public
- n est le module

La paire (e, n) constitue la clé publique utilisée pour le chiffrement.

### Déchiffrement RSA

Pour déchiffrer le message C et retrouver le message original M, on effectue l'opération inverse :

`M = C^d mod n`

Où :

- C est le message chiffré
- M est le message déchiffré (message original)
- d est l'exposant privé
- n est le même module que pour le chiffrement

La paire (d, n) constitue la clé privée utilisée pour le déchiffrement.

## Q2

Le rôle de la methode Diffie-Hellman est d'echanger une clé de manière sécurisé. Elle se base sur la complexité de factoriser des très grands nombres.