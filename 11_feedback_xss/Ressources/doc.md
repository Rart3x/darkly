# Exploit 11 - Feedback form XSS

Sur la page de feedback, il est possible d'injecter du code javascript en utilisant le champ de texte. Il semble y avoir
une tentative de filtrer les balises `<script>` mais en utilisant des lettres spécifiques, il est possible de contourner
ce filtre.

- `s` semble fonctionner
- tout comme n'importe quelle lettre du mot `script`
- ou le mot `script` lui-même.

Peut-être que la validation des entrées sur le serveur est liée à une expression régulière mal formée ?

Quoi qu'il en soit, le flag peut être récupéré via la commande suivante:

```bash
curl -s -X POST "http://192.168.56.102/?page=feedback" --data "txtName=test&mtxtMessage=s&btnSign=Sign+Guestbook" | grep -oP 'The flag is : \K[0-9a-f]{64}' | head -1
```

## Comment contrer cette attaque

Pour contrer cette attaque, il faut échapper les caractères spéciaux dans les données fournies par l'utilisateur. Par
exemple, on peut utiliser la fonction `htmlspecialchars` de PHP pour échapper les caractères spéciaux dans les balises
HTML.
Sur le client, on peut utiliser l'attribut `innerText` pour insérer du texte brut dans le DOM, ce qui empêchera
l'exécution
de code javascript.