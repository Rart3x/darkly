# Exploit 03 - Bad Cookie Encryption

## Présentation du problème

Dans cet exploit, nous avons rencontré un défi lié à la vérification des cookies sur un site web. Le cookie nommé `i_am_admin` avait une valeur initiale de `68934a3e9455fa72420237eb05902327`. Tentant de déchiffrer cette valeur avec un outil de déchiffrement MD5 (`https://md5decrypt.net`), nous avons obtenu `false`, indiquant que la valeur n'était pas correctement déchiffrée.

## Solution proposée

- **Chiffrement de la valeur `true`** : En prenant la valeur `true` comme valeur originale, avec l'outil MD5 nous obtenons : `b326b5062b2f0e69046810717534cb09`.

- **Substitution du cookie** : Remplaçons le cookie `i_am_admin` original par la nouvelle valeur cryptée (`b326b5062b2f0e69046810717534cb09`), nous obtenons ainsi le flag recherché.