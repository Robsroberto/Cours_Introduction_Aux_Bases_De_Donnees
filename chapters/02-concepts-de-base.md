## Concepts de Base des Bases de Données
Les bases de données sont des systèmes qui permettent de stocker, de gérer et de récupérer des données de manière efficace. Pour comprendre comment fonctionnent les bases de données, il est essentiel de maîtriser les concepts de base qui les sous-tendent.

### Tables, Lignes et Colonnes
Une base de données est composée de tables, qui sont des structures de données similaires à des feuilles de calcul. Chaque table est composée de lignes et de colonnes. Les lignes, également appelées enregistrements, représentent des données spécifiques, tandis que les colonnes représentent les champs ou les attributs de ces données.

Par exemple, imaginons une table qui stocke des informations sur les étudiants d'une université :
| Nom | Prénom | Age | Ville |
| --- | --- | --- | --- |
| Diallo | Amadou | 20 | Dakar |
| Sow | Fatou | 22 | Bamako |
| Traoré | Moussa | 21 | Abidjan |

Dans cet exemple, chaque ligne représente un étudiant, et les colonnes représentent les champs suivants : Nom, Prénom, Age et Ville.

### Clés Primaires et Étrangères
Les clés primaires et étrangères sont des concepts essentiels en bases de données. Une clé primaire est un champ unique qui identifie chaque enregistrement dans une table. Elle doit être unique et non nulle.

Une clé étrangère, en revanche, est un champ qui fait référence à la clé primaire d'une autre table. Les clés étrangères permettent de créer des relations entre les tables.

Par exemple, imaginons deux tables : une table "Étudiants" et une table "Cours" :
| Étudiant_ID | Nom | Prénom | Age | Ville |
| --- | --- | --- | --- | --- |
| 1 | Diallo | Amadou | 20 | Dakar |
| 2 | Sow | Fatou | 22 | Bamako |
| 3 | Traoré | Moussa | 21 | Abidjan |

| Cours_ID | Nom_Cours | Étudiant_ID |
| --- | --- | --- |
| 1 | Mathématiques | 1 |
| 2 | Physique | 2 |
| 3 | Informatique | 3 |

Dans cet exemple, la table "Étudiants" a une clé primaire "Étudiant_ID", tandis que la table "Cours" a une clé étrangère "Étudiant_ID" qui fait référence à la clé primaire de la table "Étudiants".

### Relations entre les Tables
Les relations entre les tables sont essentielles en bases de données. Il existe trois types de relations :

*   **Relation un-à-un** : une ligne dans une table est associée à une ligne dans une autre table.
*   **Relation un-à-plusieurs** : une ligne dans une table est associée à plusieurs lignes dans une autre table.
*   **Relation plusieurs-à-plusieurs** : plusieurs lignes dans une table sont associées à plusieurs lignes dans une autre table.

Par exemple, imaginons deux tables : une table "Étudiants" et une table "Cours" :
| Étudiant_ID | Nom | Prénom | Age | Ville |
| --- | --- | --- | --- | --- |
| 1 | Diallo | Amadou | 20 | Dakar |
| 2 | Sow | Fatou | 22 | Bamako |
| 3 | Traoré | Moussa | 21 | Abidjan |

| Cours_ID | Nom_Cours | Étudiant_ID |
| --- | --- | --- |
| 1 | Mathématiques | 1 |
| 2 | Physique | 1 |
| 3 | Informatique | 2 |

Dans cet exemple, un étudiant peut suivre plusieurs cours, ce qui représente une relation un-à-plusieurs.

### Principes de Normalisation des Données
La normalisation des données est le processus de réorganisation des données pour minimiser les redondances et les incohérences. Il existe plusieurs règles de normalisation, notamment :

*   **Première forme normale (1FN)** : chaque cellule de la table ne contient qu'une valeur unique.
*   **Deuxième forme normale (2FN)** : chaque non-clé dépend de la clé primaire.
*   **Troisième forme normale (3FN)** : si une table est en 2FN, et si une non-clé dépend d'une autre non-clé, alors elle doit être placée dans une table séparée.

Par exemple, imaginons une table qui stocke des informations sur les commandes :
| Commande_ID | Date_Commande | Nom_Client | Adresse_Client | Produit | Quantité |
| --- | --- | --- | --- | --- | --- |
| 1 | 2022-01-01 | Diallo | Dakar | Ordinateur | 2 |
| 2 | 2022-01-02 | Sow | Bamako | Imprimante | 1 |
| 3 | 2022-01-03 | Traoré | Abidjan | Scanner | 3 |

Cette table n'est pas normalisée, car elle contient des redondances. Pour la normaliser, nous pouvons la diviser en plusieurs tables :
| Commande_ID | Date_Commande | Client_ID |
| --- | --- | --- |
| 1 | 2022-01-01 | 1 |
| 2 | 2022-01-02 | 2 |
| 3 | 2022-01-03 | 3 |

| Client_ID | Nom_Client | Adresse_Client |
| --- | --- | --- |
| 1 | Diallo | Dakar |
| 2 | Sow | Bamako |
| 3 | Traoré | Abidjan |

| Produit_ID | Nom_Produit |
| --- | --- |
| 1 | Ordinateur |
| 2 | Imprimante |
| 3 | Scanner |

| Commande_ID | Produit_ID | Quantité |
| --- | --- | --- |
| 1 | 1 | 2 |
| 2 | 2 | 1 |
| 3 | 3 | 3 |

Dans cet exemple, nous avons normalisé la table en la divisant en plusieurs tables, ce qui a minimisé les redondances et les incohérences.

## Exemple de Code
Voici un exemple de code SQL qui crée les tables ci-dessus :
```sql
CREATE TABLE Clients (
  Client_ID INT PRIMARY KEY,
  Nom_Client VARCHAR(255),
  Adresse_Client VARCHAR(255)
);

CREATE TABLE Produits (
  Produit_ID INT PRIMARY KEY,
  Nom_Produit VARCHAR(255)
);

CREATE TABLE Commandes (
  Commande_ID INT PRIMARY KEY,
  Date_Commande DATE,
  Client_ID INT,
  FOREIGN KEY (Client_ID) REFERENCES Clients(Client_ID)
);

CREATE TABLE Lignes_Commande (
  Commande_ID INT,
  Produit_ID INT,
  Quantité INT,
  FOREIGN KEY (Commande_ID) REFERENCES Commandes(Commande_ID),
  FOREIGN KEY (Produit_ID) REFERENCES Produits(Produit_ID)
);
```
## Points clés
*   Les bases de données sont des systèmes qui permettent de stocker, de gérer et de récupérer des données de manière efficace.
*   Les tables sont des structures de données similaires à des feuilles de calcul, composées de lignes et de colonnes.
*   Les clés primaires et étrangères sont des concepts essentiels en bases de données, qui permettent de créer des relations entre les tables.
*   Les relations entre les tables sont essentielles en bases de données, et il existe trois types de relations : un-à-un, un-à-plusieurs et plusieurs-à-plusieurs.
*   La normalisation des données est le processus de réorganisation des données pour minimiser les redondances et les incohérences.
*   Les règles de normalisation incluent la première forme normale (1FN), la deuxième forme normale (2FN) et la troisième forme normale (3FN).