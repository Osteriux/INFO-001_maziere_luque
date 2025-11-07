# INFO-001_maziere_luque

> Xavier Mazière  
> Mattéo Luque

## Q1 - Principe de fonctionnement de RSA

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

## Q2 - Rôle de la méthode Diffie-Hellman

Le rôle de la methode Diffie-Hellman est d'echanger une clé de manière sécurisé. Elle utilise des propriétés mathématiques des modulos pour permettre à deux parties de générer une clé secrète partagée, même si elles communiquent sur un canal non sécurisé.

## Q3 - Informations importantes d'un certificat

Un certificat numérique contient plusieurs informations importantes, notamment :

- Le titulaire du certificat (personne ou organisation)
- Le hash du certificat pour vérifier son intégrité
- La clé publique associée au titulaire
- La période de validité du certificat (date de début et date d'expiration)
- L'autorité de certification qui a émis le certificat
