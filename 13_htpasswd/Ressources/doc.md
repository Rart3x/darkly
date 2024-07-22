# Exploit 13 - htaccess

Tout site voulant être indexé convenablement par les moteurs de recherche doit fournir un fichier `robots.txt` à la
racine de son site. Il est donc naturel de chercher ce fichier pour trouver des informations cachées.

L'url http://192.168.56.101/robots.txt nous informe de l'existence de deux urls qui ne sont pas indexées:

- /whatever
- /.hidden

On se rend vite compte que même si ces pages ne sont pas indexées, elles sont accessibles.

Ainsi sous http://192.168.56.101/whatever/htpasswd on trouve un fichier htpasswd qui contient les informations de
connexion

- root:437394baff5aa33daa618be47b75cb49

Cela ressemble à un hash md5, il est réversible:
avec l'outil https://md5.gromweb.com/?md5=437394baff5aa33daa618be47b75cb49,
on peut inverser le hash en _qwerty123@_

Ces informations de connexion ne fonctionnent pas sur la page de connexion, il doit y avoir une page d'administration:
On peut la trouver à l'url http://192.168.56.101/admin.

Enfin, la récupération du flag peut être automatisée avec la commande:

```bash
curl -s -X POST http://192.168.56.102/admin/ --data "username=root&password=qwerty123@&Login=Login" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```

Pour contrer cette attaque, il ne faut pas considérer les fichiers cachés comme étant sécurisés. Il est préférable de
mettre en place une authentification pour accéder à ces fichiers.