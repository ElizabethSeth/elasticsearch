🎬 Projet d’Ingestion & Visualisation de Données de Films

Stack Elastic : Elasticsearch • Logstash • Kibana

📌 Objectif du Projet

Créer un pipeline complet de traitement des données cinématographiques permettant :

✅ Lecture d’un flux de films
✅ Nettoyage & enrichissement des données
✅ Indexation automatique dans Elasticsearch
✅ Construction de visualisations d’analyse dans Kibana

📊 Ce projet permet de mieux comprendre les genres, réalisateurs et tendances du cinéma.

🛠️ Architecture
flowchart LR
  A[movies.json] -->|Clean + Transform| B(Logstash)
  B -->|Indexation| C[Elasticsearch]
  C -->|Visualisation| D[Kibana Dashboard]

🔧 1️⃣ Logstash — Pipeline d’Ingestion

📄 Fichier : movies_pipeline.conf

✅ Transformations appliquées
Transformation	Description	Objectif
🔄 Conversion de types	rating → float, year → int	structuration des données
🕙 Création champ decade	Ex : 2013 → 2010s	analyse temporelle
⏱ Conversion durée	running_time_secs → duration_min	lisibilité
🎬 Normalisation réalisateur	Ajout director_name	regroupements plus précis
🚫 Filtrage qualité	Suppression films avec rating < 5	dataset pertinent

📌 Résultat → Dataset propre, enrichi & exploitable ✅

📦 2️⃣ Indexation Elasticsearch

Index créé automatiquement :

movies-%{+YYYY.MM.dd}


Vérification :

curl -k -u "elastic:<PW>" "https://localhost:9200/_cat/indices/movies-*?v"
curl -k -u "elastic:<PW>" "https://localhost:9200/movies-*/_count?pretty"


📌 Exemple d’état obtenu :

Champ	Valeur
Nombre de films	≈ 4850
Espace total	≈ 4 Mo

🎯 Seuls les films bien notés sont indexés → signal positif 💡

📊 3️⃣ Dashboard Kibana — Visualisations

Le tableau de bord inclut 4 visualisations pertinentes ✅

Visualisation	Description	Insight
📈 Bar chart — Movies Count by Genre	Top genres par nombre de films	La majorité : Drama & Comedy
🍩 Donut — Best Directors (avg rating)	Top réalisateurs les mieux notés	Chaplin & Kurosawa brillent ⭐
🧱 Treemap — Répartition des réalisateurs par genre	Qui réalise quoi ?	Bonne diversité selon les genres
🎭 Stacked Bar — Genres par acteur	Acteurs multi-genres	Robert De Niro & Bruce Willis dominent