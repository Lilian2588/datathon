# Vel'ogre : La Ville à Vélo Prioritaire, la 'référence' du Datathon 2026

Offrir une solution pour faire passer le ressenti subjectif des cyclistes lyonnais en un plan d’action objectif pour la Métropole. En croisant les signalements des citoyens (Points Rouges) à la réalité du trafic pour établir un Indice de Priorité pouvant apporter des solutions aux interventions à privilégier.

## Structure du Projet

L'organisation du dépôt suit les étapes logiques du traitement de données :

* data_coord/ : Données géographiques, signalements Points Rouges et enquêtes EPCI.
* data_flux/ : Données brutes de trafic (mesures, sites et canaux de comptage).
* data_travaux/ : Registre des chantiers en cours pour le filtrage spatial.
* src/ : Coeur algorithmique du projet regroupant les notebooks de traitement.
* visualisation/ : Présentation des données traités sous formes de dashboard.

## Chaîne de Traitement (src/)

La pipeline de données se décompose en notebooks :

### 1. Filtrage et Nettoyage (filtre_travaux.ipynb)
Ce module comporte le filtrage et nettoyage initiaux des données brutes et le croisement spatial avec l’état des chantiers. L’idée est de retirer les signalements temporaires en lien direct avec ces travaux pour ne conserver que les problèmes structurels.

### 2. Analyse Thématique (nlp_points_rouge.ipynb)
Ce notebook traite les commentaires libres pour catégoriser les problèmes mis en avant. Chaque incident identifié dans les signalements est noté pour son urgence sécuritaire et sa facilité de résolution.

### 3. Analyse du Ressenti (questionnaire.ipynb)
Ce module traite les réponses aux enquêtes usagers par commune pour réaliser une synthèse statistique du ressenti global des cyclistes. Il doit permettre de pondérer la priorité d’intervention selon un contexte local.

### 4. Harmonisation du Trafic (traitement_flux.ipynb)

Cette section regroupe la fusion et le géocodage des différentes sources de comptage vélo (Métropole de Lyon et association La Ville à Vélo), afin d’élaborer une base de flux unifiée.

## Visualisation et Dashboard (visualisation/)

La partie visualisation permet d’actionner les résultats pertinents via un affichage cartographique :

* Préparation des données (visualisation.ipynb) : Ce notebook transforme les résultats du croisement complet en fichiers légers (CSV/GeoJSON), optimisés pour l’affichage web. Y compris des agrégations par commune, notamment.
* Interface Interactive (index.html et style.css) : Un dashboard basé sur une carte interactive permet de filtrer les incidents par priorité, par catégorie de problème ou par commune.
* Analyse Spatiale : La visualisation fait la superposition des points de signalement prioritaires avec les zones de flux important afin d’identifier visuellement les points noirs du réseau cyclable.

## L’Indice de Priorité 

Le score d’importance globale (0-100) objectivé de l’intervention fusionne quatre facteurs :
* Flux de Trafic (40%) : Priorité aux zones ayant une forte fréquentation par les cyclistes.
* Urgence (30%) : Gravité des problèmes de sécurité identifiée dans le cadre de l’analyse thématique.
* Proximité (20%) : Fiabilité de la donnée liée à la distance la plus proche au compteur.
* Facilité (10%) : Identification des réparations rapides (Quick Wins).
* 
## Stack Technique
* Traitement de données : PySpark, Pandas.
* Analyse Textuelle : NLP par dictionnaire de mots-clés.
* Cartographie et Web : HTML, CSS, JavaScript (Leaflet).
* Géocodage : API Adresse Data Gouv.

---
Projet réalisé par l'équipe Vel'ogre : Tristan Bellet, Cédric Guéguénou, Rami Messeoudi, Laëtitia Montbarbon, Lilian Saglibene.
