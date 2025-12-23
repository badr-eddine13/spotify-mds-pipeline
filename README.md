# spotify-mds-pipeline
📌 Aperçu du projet

Ce projet présente un pipeline complet de data engineering en temps réel pour l’analytique musicale de Spotify, basé sur la Modern Data Stack (MDS).

Nous simulons des données musicales en streaming — incluant les écoutes de chansons, les auditeurs, les régions et les types d’appareils — puis nous construisons un pipeline entièrement automatisé, depuis l’ingestion des données jusqu’à leur visualisation.

Une fois le pipeline lancé, chaque composant fonctionne automatiquement :
simulation des données → streaming via Kafka → stockage dans Snowflake → transformation avec DBT → visualisation dans Power BI
