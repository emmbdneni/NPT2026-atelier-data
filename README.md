
# MaifStery - Murder Mystery SQL 🕵️‍♀️

Bienvenue dans cet atelier qui vous permettra découvrir les bases de données SQL à travers une enquête policière !  
Votre mission : **résoudre un crime en interrogeant, non pas des suspects, mais une base de données**.

## 📚 1. Avant de commencer, une base de données, c'est quoi ? 
Une **base de données** est un système qui permet d'accéder facilement à un ensemble organisé de données, de les manipuler et de les mettre à jour.  
Comme montré ci-dessous dans le schéma, le **client** (un site web, une application, etc.) envoie une requête à une **API** (un serveur) qui va récupérer et/ou mettre à jour les données associées dans la base de données.

**Maintenant que vous êtes en possession des bases (de données), il est grand temps de se plonger dans notre affaire.**

## 🕵️ 2. Scénario
Un **meurtre** a été commis à **MAIF City**, capitale française des assurances, le **26 janvier 2026**.  
La victime travaillait dans une grande compagnie d’assurance et enquêtait sur une fraude massive.  

## 🗺 3. Schéma de la base de données
Voici un exemple simple de la modélisation de la base de données relative à notre enquête.  

La base de données contient 5 **tables** :
- **crime_scene_report** : le rapport d'enquête avec les informations de base (date, type de crime, description, ville).
- **interview** : les transcripts des interrogatoires
- **person** : la liste des personnes interrogées et/ou inscrites à la salle avec leur nom et leur adresse. 
- **get_fit_now_check_in** et **get_fit_now_member** : informations sur les pratiques sportives des suspects avec notamment leur type d'abonnement, les dates auxquelles ils se sont rendus à la salle...
Ces tables sont liées par des identifiants (`person_id`, `membership_id`...) pour permettre des requêtes complexes.

Ces tables contiennent également plusieurs **colonnes** dans lesquelles on va venir regrouper l'information. 

Voici quelques exemples du contenu des tables et de leurs colonnes sous forme de tableaux : 


## 🛠 4. Commandes SQL utiles
Pour vous aider à commencer, voici quelques **requêtes** qui vous seront utiles dans le cadre de votre enquête
| Commande      | Description                          | Exemple |
|---------------|--------------------------------------|---------|
| `SELECT *`    | Affiche toutes les colonnes d’une table | `SELECT * FROM crime_scene_report;` |
| `SELECT col`  | Affiche uniquement certaines colonnes | `SELECT name, address_number, address_name FROM person;` |
| `WHERE`       | Filtre les résultats selon une condition | `SELECT * FROM crime_scene_report WHERE city = 'MAIF City'|
| `LIKE`        | Recherche avec un motif (pattern) | `SELECT * FROM person WHERE name LIKE '%Martin%';` 
| `ORDER BY`    | Trie les résultats (ASC ou DESC) | `SELECT name, address_number, address_name FROM person ORDER BY name DESC;` |
| `JOIN`        | Relie deux tables via une clé | `SELECT * FROM person JOIN get_fit_now_member ON person.id = get_fit_now_member.id;` |

### Les types de données courant : 
**INTEGER** : pour les nombres entiers (ex. âge, identifiant).
**TEXT** : pour du texte (ex. nom, adresse, description).
Ces types permettent à la base de savoir comment stocker et comparer les données.
Avec INTEGER, on peut faire des calculs (age > 30). 
Avec TEXT, on peut faire des recherches (city LIKE "%MAIF City%")

## 🚀 5. Si vous êtes prêt... c'est le moment de lancer la murder party !

### Étape 1 : Initialiser les données

Récupérez le fichier nomdufichier
Copiez/collez son contenu entier dans "Input" sur Online SQL Editor
Cliquez sur "Run SQL"
Supprimez tout ce qui se trouve dans "Input"

### Étape 2 : Lire des données grâce à SQL

Récupérez les données du rapport d'enquête
#### 🔍 Pour rappeler voici les indices qui sont à votre disposition pour commencer l'aventure	 :
- Le crime a eu lieu le **26 janvier 2026**.
- Le lieu : **MAIF City**.
- Le type de crime : **meurtre**

Solution

SELECT * FROM crime_scene_report WHERE city = "MAIF City" AND type = "meurtre" AND date = 20260126

2. Récupérez l'id du témoin 1

Solution

SELECT * FROM person WHERE address_street = "Northwestern Dr" ORDER BY address_number DESC

3. Interrogez le témoin 1

Solution

SELECT * FROM interview WHERE person_id = 14887

4. Récupérez l'id du témoin 2 (Annabel)

Solution

SELECT * FROM person WHERE name LIKE "Annabel%" AND address_street= "Franklin Ave"

5. Interrogez le témoin 2 (Annabel)

Solution

SELECT * FROM interview WHERE person_id = 16371

6. Allez à la salle de gym pour creuser les pistes évoquées par les témoins

Solution

SELECT * FROM get_fit_now_member JOIN get_fit_now_check_in on id = membership_id WHERE check_in_date = 20260109 AND membership_status = "gold" AND id LIKE "%48Z%"

### Étape 3 : Vérifier votre réponse

Réalisez une requête d'insert avec le nom du coupable puis vérifiez votre solution
INSERT INTO solution VALUES (1, 'Insérer le nom de votre suspect ici');        
SELECT value FROM solution;

Solution

INSERT INTO solution VALUES (1, "Jeremy Bowers");
SELECT value FROM solution;

### Résumé
À la fin de l'atelier, chaque participant aura :

Lu et compris du SQL simple
Découvert du SQL plus complexe
Ajouté une nouvelle donnée en SQL

## 🏁 6. Remerciements
Merci d'avoir participé à cet atelier et d'avoir joué le jeu jusqu'au bout !  **Le rideau tombe sur MAIF City**… Mais votre voyage avec SQL ne fait que commencer. Chaque base cache ses secrets, et vous avez désormais les clés pour les révéler.

Ce projet est inspiré de [SQL Murder Mystery](https://mystery.knightlab.com/), créé par **Joon Park**, **Cathy He** et **Joe Germuska**.  
Cette enquête s’inspire d’un crime fictif dans la ville de Terminal City.  
Code original sous licence **MIT**.  
Texte et contenu originaux sous licence **Creative Commons CC BY-SA 4.0**.  
