# INFO-001_maziere_luque

> Xavier Mazière  
> Mattéo Luque

## Q1 - Principe de fonctionnement de RSA

### Chiffrement RSA

Pour chiffrer un message M en utilisant RSA, on effectue le calcul suivant :

$$C = M^e \bmod n$$

Où :

- M est le message en clair (converti en valeur numérique)
- C est le message chiffré
- e est l'exposant public
- n est le module

La paire (e, n) constitue la clé publique utilisée pour le chiffrement.

### Déchiffrement RSA

Pour déchiffrer le message C et retrouver le message original M, on effectue l'opération inverse :

$$M = C^d \bmod n$$

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

## Q4 - Étapes d'authentification HTTPS avec chaîne de certificats

1. Bob se connecte en HTTPS à <www.alice.com>
2. Le serveur envoie son certificat, contenant celui de ca1
3. Bob vérifie que l'issuer du certificat de ca1 est dans son truststore
4. Bob vérifie la signature de ca1 avec la clé publique de root-ca
5. Bob vérifie la validité et la non-révocation du certificat ca1
6. Bob vérifie la signature d'Alice avec la clé publique de ca1
7. Bob vérifie la validité et la non-révocation du certificat d'Alice
8. Bob vérifie que le nom de domaine correspond (<www.alice.com>)
9. Bob extrait la clé publique d'Alice
10. Échange de clé de session et communication chiffrée établie

## Q5 - Génération d'une pair de clés RSA

On entre les commandes suivantes pour générer la pair de clés RSA et afficher les informations des clés générées :

```txt
[etudiant@tls-ca-luquem ~]$ openssl genpkey -algorithm RSA -out rsa_keys.pem -pkeyopt rsa_keygen_bits:1024
................................................................................++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
......++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
[etudiant@tls-ca-luquem ~]$ openssl rsa -in rsa_keys.pem -text -noout
Private-Key: (1024 bit, 2 primes)
...
```

Le module (n) est de taille 1024 bits + 8 bits à 0 :

```txt
modulus:
    00:bd:24:c1:dd:8b:0b:0d:bd:65:aa:c2:9d:fb:34:
    40:bb:75:d2:82:ab:c2:3e:b6:01:25:ff:1e:34:57:
    b3:ef:9e:f0:c7:0c:93:aa:80:da:52:73:e1:e8:53:
    e0:77:48:d7:ad:85:99:93:27:00:d6:ce:ec:9a:e0:
    63:2d:c2:50:26:5d:4e:64:6b:9d:0a:e1:cf:93:8e:
    f0:5b:25:17:84:67:42:fa:18:f5:64:9c:5b:6c:51:
    3e:fd:d5:6d:50:12:af:bd:72:b4:5f:21:0b:d7:d8:
    96:fb:8a:91:b0:d6:f5:a7:15:52:f1:26:80:71:2c:
    b9:b9:a0:83:7d:d0:cd:fa:57
```

Comme rappelé ci-dessus, le calcul pour chiffre un message M avec la clé publique (e, n) est :
$$C = M^e \bmod n$$

L'exposant public n'est pas difficile à "deviner", puisqu'il est fourni dans la clé publique (donc pas secret). Ce n'est pas un problème puisque le décryptage ne l'utilise pas.

## Q6 - Chiffrer une clé

On peut encrypter une clé RSA avec un mot de passe en utilisant la commande suivante (avec AES-128 dans ce cas-ci) :

```txt
[etudiant@tls-ca-luquem ~]$ openssl rsa -in rsa_keys.pem -aes128 -out rsa_keys_cyphered.pem
writing RSA key
Enter pass phrase:
Verifying - Enter pass phrase:
```

Chiffrer la clé publique n'a pas d'intérêt, puisqu'elle est destinée à être partagée publiquement. En revanche, chiffrer la clé privée avec un mot de passe ajoute une couche de sécurité supplémentaire, puisque même si la machine est compromise, un attaquant ne pourra pas utiliser la clé privée sans connaître le mot de passe.

## Q7 - Encodage

Comme on peut le voir à l'extension utilisée (.pem), les clés sont au format PEM (Privacy Enhanced Mail). Ce format utilise l'encodage Base64 pour représenter les données binaires de manière textuelle (représnetation ASCII), ce qui facilite leur transmission et leur stockage dans des fichiers texte. Le format PEM inclut également des en-têtes et des pieds de page pour indiquer le type de contenu.

## Q8 - Clé publique

En utilisant la commande suivante, on peut afficher la clé publique, contenant bien le module (n) et l'exposant public (e) :

```txt
[etudiant@tls-ca-luquem ~]$ openssl rsa -pubin -in pub.pem -text -noout
Public-Key: (1024 bit)
Modulus:
    00:bd:24:c1:dd:8b:0b:0d:bd:65:aa:c2:9d:fb:34:
    40:bb:75:d2:82:ab:c2:3e:b6:01:25:ff:1e:34:57:
    b3:ef:9e:f0:c7:0c:93:aa:80:da:52:73:e1:e8:53:
    e0:77:48:d7:ad:85:99:93:27:00:d6:ce:ec:9a:e0:
    63:2d:c2:50:26:5d:4e:64:6b:9d:0a:e1:cf:93:8e:
    f0:5b:25:17:84:67:42:fa:18:f5:64:9c:5b:6c:51:
    3e:fd:d5:6d:50:12:af:bd:72:b4:5f:21:0b:d7:d8:
    96:fb:8a:91:b0:d6:f5:a7:15:52:f1:26:80:71:2c:
    b9:b9:a0:83:7d:d0:cd:fa:57
Exponent: 65537 (0x10001)
```

Avoir un fichier à part pour la clef publique est pratique car cela permet de faciliter son partage sans resquer de transmettre des informations de la clé privée.

## Q9 - Chiffrement RSA

Pour envoyer un massage confidentiel avec RSA il faut le chiffrer à l'aide de la clé publique de la personne avec qui on souhaite communiquer.
