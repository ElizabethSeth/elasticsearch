🎬 Projet Elasticsearch : Ingestion & Visualisation de Films
👨‍🎓 Présentation

Ce projet a été réalisé dans le cadre du module Big Data & Elastic Stack.
L’objectif était de mettre en place un pipeline complet pour :

✅ Ingérer des données de films
✅ Les transformer et filtrer automatiquement
✅ Les indexer dans Elasticsearch
✅ Construire un dashboard interactif dans Kibana

🛠️ Stack Technique
Technologie	Rôle
Logstash	Pipeline ETL : lecture → transformation → envoi
Elasticsearch	Moteur de recherche et stockage
Kibana	Visualisation et analyse de données
📂 1️⃣ Logstash — Ingestion & Transformations
✅ Fichier de configuration utilisé : movies_pipeline.conf

🔹 Logstash lit un fichier NDJSON : chaque ligne = un film
🔹 Transformations appliquées :

Transformation	Exemple	Objectif
Conversion des types	rating → float, year → integer	Cohérence des données
Extraction de la décennie	2013 → 2010s	Faciliter l’analyse par période
Conversion durée	running_time_secs → duration_min	Lecture humaine
Enrichissement	director_name = directors[0]	Regroupements plus simples
Filtrage qualité	films avec rating < 5 supprimés	Conserver les meilleurs films

🧠 Résultat : un dataset propre, enrichi et exploitable.

🗂️ 2️⃣ Indexation Elasticsearch

✅ Index créé automatiquement :

movies-%{+YYYY.MM.dd}


📌 Vérification en CLI :

curl -k -u "elastic:<PW>" "https://localhost:9200/_cat/indices/movies-*?v"
curl -k -u "elastic:<PW>" "https://localhost:9200/movies-*/_count?pretty"