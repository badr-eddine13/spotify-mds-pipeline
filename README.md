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
