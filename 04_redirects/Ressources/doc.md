# Exploit 04 - Redirects

## Présentation du problème

Dans cet exploit, nous avons manipulé les redirections d'un lien sur un site web pour trouver un flag caché. Plus précisément, nous avons modifié l'URL de redirection d'un lien Twitter vers Google.

### Avant Modification

`<a href="index.php?page=redirect&amp;site=twitter" class="icon fa-twitter"></a>`

### Après Modification

`<a href="index.php?page=redirect&amp;site=www.google.com" class="icon fa-twitter"></a>`

Nous avons changé l'attribut `site` dans l'URL de redirection de `twitter` à `www.google.com`. Cette modification a eu pour effet de changer la destination de la redirection vers Google.

### Résultat

En modifiant la redirection, nous avons pu découvrir le flag recherché. Cette manipulation de redirection illustre comment les petits changements dans les paramètres d'un lien peuvent avoir un impact significatif sur le flux de navigation utilisateur et potentiellement révéler des informations cachées ou des fonctionnalités non apparentes.

## Protection contre ce genre de cas

Pour protéger contre ce genre de vulnérabilité, plusieurs mesures peuvent être prises :

- **Validation stricte des entrées** : Assurez-vous que toutes les entrées utilisateur sont validées et nettoyées pour éviter toute injection de code malveillant.
  
- **Utilisation de fonctions de validation côté serveur** : Au lieu de confier la validation des entrées uniquement au client, utilisez des fonctions côté serveur pour filtrer et valider les données reçues.
  
- **Limitation des redirections autorisées** : Restreindre les destinations de redirection à un ensemble limité d'URL connues et sécurisées peut aider à prévenir les redirections non autorisées.

```php
{
    destinations = array("facebook", "twitter", "instagram");

    if(in_array($destination, $destinations)) {
        header("Location: index.php?page=$destination");
        exit();
    } else
        echo "Redirection vers cette page n'est pas autorisée.";
}
```