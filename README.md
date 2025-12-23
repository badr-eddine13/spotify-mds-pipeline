# spotify-mds-pipeline
📌 Aperçu du projet

Ce projet présente un pipeline complet de data engineering en temps réel pour l’analytique musicale de Spotify, basé sur la Modern Data Stack (MDS).

Nous simulons des données musicales en streaming — incluant les écoutes de chansons, les auditeurs, les régions et les types d’appareils — puis nous construisons un pipeline entièrement automatisé, depuis l’ingestion des données jusqu’à leur visualisation.

Une fois le pipeline lancé, chaque composant fonctionne automatiquement :
simulation des données → streaming via Kafka → stockage dans Snowflake → transformation avec DBT → visualisation dans Power BI

🏗️ Architecture

![Image](https://github.com/user-attachments/assets/6d198b9e-8b26-4b5b-a4f8-15d582461e64)

Flux du pipeline :

1. Simulateur de données → Génère de fausses données de streaming Spotify (utilisateur, piste, région, appareil).

2. Producteur Kafka → Diffuse les données en temps réel vers les topics Kafka.

3. Consommateur Kafka → Consomme les données et les stocke à l’état brut dans MinIO (stockage compatible S3).

4. Airflow → Orchestration du chargement des données de MinIO → Snowflake (couche Bronze).

5. Snowflake → Stocke et gère les données selon les couches Bronze → Silver → Gold.

6. DBT → Nettoie, transforme et construit des modèles analytiques prêts à l’emploi directement dans Snowflake.

7. Power BI → Se connecte aux tables Gold de Snowflake pour créer des tableaux de bord interactifs et des analyses approfondies.


⚡ Stack technologique

Python (Faker) → Simulation des données

Apache Kafka → Streaming de données en temps réel

MinIO → Stockage objet (compatible S3)

Snowflake → Entrepôt de données cloud

DBT → Transformations, tests et modélisation des données

Apache Airflow → Orchestration et planification des DAGs

Power BI → Tableaux de bord et analyses décisionnelles

Docker & docker-compose → Environnement conteneurisé


✅ Fonctionnalités clés

Pipeline entièrement automatisé — de bout en bout, de l’ingestion des données jusqu’aux analyses

Streaming en temps réel grâce à Kafka

Architecture Medallion (Bronze → Silver → Gold) implémentée dans Snowflake

DBT pour les transformations et les tests (modèles SQL propres, modulaires et maintenables)

Tableaux de bord Power BI présentant les écoutes par région, les tendances des chansons et des insights sur les auditeurs

Déploiement conteneurisé pour garantir la reproductibilité

Pipeline CI/CD avec automatisation des tests DBT


# ⚙️ Implémentation étape par étape
1. Simulation des données

Génération de fausses données de streaming Spotify à l’aide de Python + Faker.

Champs de données : user_id, track_name, artist, region, device_type, timestamp, duration.

Simulation d’un flux continu d’écoutes musicales.

2. Streaming avec Kafka

Utilisation d’un Producteur Kafka pour envoyer les données vers des topics Kafka en temps réel.

Chaque message représente un événement d’écoute d’une chanson.

Le Consommateur Kafka stocke ces événements sous forme de fichiers JSON bruts dans MinIO.

3. Orchestration avec Airflow

DAG 1 : Chargement des données brutes depuis MinIO → Snowflake (couche Bronze).

DAG 2 : Déclenchement des exécutions DBT pour construire les modèles Silver et Gold.

4. Entrepôt de données Snowflake

Couche Bronze : Données brutes ingérées directement depuis MinIO.

Couche Silver : Données nettoyées et standardisées.

Couche Gold : Insights agrégés tels que :

Top artistes

Régions les plus écoutées

Utilisation des appareils

5. Transformations avec DBT

Modèles de staging : Nettoyage des noms de colonnes, gestion des valeurs nulles, standardisation des timestamps.

Marts de données :

Faits : écoutes (plays), auditeurs (listeners)

Dimensions : pistes, artistes, appareils, régions

Tests et documentation automatisés via :

dbt test

dbt docs generate

6. Visualisation dans Power BI

Connexion directe à la couche Gold de Snowflake.

Création de visualisations interactives :

🎵 Top artistes / chansons par nombre d’écoutes

🌎 Carte thermique régionale (États des États-Unis)

📈 Tendances dans le temps (graphique en ligne)

💽 Répartition par type d’appareil (diagramme en anneau)

<img width="704" height="391" alt="Image" src="https://github.com/user-attachments/assets/e3c4dc0c-ee9f-4329-88a0-93243799332a" />

📊 Livrables finaux

Pipeline de streaming de données Spotify en temps réel

Architecture Medallion propre dans Snowflake (Bronze → Silver → Gold)

Projet de transformation DBT (staging, marts, gold)

Orchestration automatisée avec Airflow

Tableau de bord Power BI interactif

🧠 Concepts abordés

Ingestion de données en temps réel (Kafka)

Architecture Medallion (Bronze → Silver → Gold)

Modélisation des données avec DBT

Entrepôt de données dans Snowflake

Orchestration des workflows avec Airflow

Visualisation des données avec Power BI
