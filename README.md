# FCSC 2023 Un truc qui cloche

Nous avons retrouvé un message qui a été chiffré par un vieux serveur avec RSA-CRT. Malheureusement, le serveur est en très mauvais état, il n’est possible de réaliser qu’une unique signature (ou un déchiffrement, c’est la même opération) mais cette opération se passe mal. Nous pensons qu’une erreur est introduite lors du calcul de l’exponentiation modulaire d’un des résidus modulaires.

Nous comptons sur vous pour récupérer la clé permettant de déchiffrer le message.

Le serveur réalise le chiffrement de la manière suivante (en Python) :

```python
m = int.from_bytes(b"Test message", "big")
c = pow(m, e, n)
```
Le serveur réalise le déchiffrement (ou la signature) de la manière suivante :

```python
n = p * q
dp = d % (p - 1)
dq = d % (q - 1)
cp = pow(m, dp, p)
cq = pow(m, dq, q)
_, a, b = egcd(p, q) # Extended GCD
m = (a * p * cq + b * q * cp) % n
```

Pour convertir le message en suite d’octets :
```python
m = m.to_bytes((m.bit_length() + 7) // 8, "big")
```



Auteur : Ker


Origine : [Un truc qui cloche](https://hackropole.fr/fr/challenges/hardware/fcsc2023-hardware-un-truc-qui-cloche/)


-----------

## Connectez vous en WEBSSH
> http://localhost

#### tentez 
> nc un-truc-qui-cloche.cyrhades.fr:4000

-----------

## Ou directement avec netcat
> nc localhost:4000


-----------


## Installation manuel
Vous n'utilisez pas l'application **les CTFs de Cyrhades** ? C'est dommage !
Mais voici comment installer ce CTF manuellement :

> git clone https://github.com/Hack-Oeil/fcsc2023-hardware-un-truc-qui-cloche.git

> cd fcsc2023-hardware-un-truc-qui-cloche


-----------


## Sur le site officiel hackropole.fr
> https://hackropole.fr/fr/challenges/hardware/fcsc2023-hardware-un-truc-qui-cloche/