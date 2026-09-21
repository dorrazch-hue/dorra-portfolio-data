# Dorra — Data Engineer

Formation Data Engineer · Spécialisation NLP et bases de données vectorielles

Je construis des pipelines de données et des systèmes IA de bout en bout — de l'ingestion au déploiement en production. Voici les projets réalisés pendant ma formation, sur des sujets variés : NLP, streaming temps réel, MLOps, ELT cloud et sécurité des données.

---

## Projets

---

### Du POC au MVP — Chatbot RAG Puls-Events
`GCP` `Vertex AI` `LangChain` `ChromaDB` `Gemini 1.5 Pro` `Langfuse` · *Août 2026*

Puls-Events avait un POC fonctionnel mais pas d'architecture pour le passer en production. J'ai conçu l'étude de design complète du MVP : analyse des besoins, choix de la stack cloud, architecture technique, backlog priorisé, registre des risques, conformité RGPD et estimation des coûts.

Le vrai sujet de ce projet n'était pas technique — c'était de prendre des décisions d'architecture justifiées avec des contraintes réelles (budget, charge incertaine, RGPD) et de les structurer dans un plan de projet tenable sur 12 semaines.

**Points clés :**
- Architecture RAG avec persistance vectorielle réfléchie : ChromaDB client-serveur + GCS en MVP, migration Vertex AI Vector Search planifiée en production
- Stratégie de scalabilité documentée (instances Cloud Run, cache LRU, fallback modèle)
- OPEX estimé à ~210 €/mois pour 1 000 utilisateurs, avec plan d'optimisation budgétaire (cache, batching, fallback Gemini 1.5 Flash)
- RGPD : consentement opt-in, historique 30 jours max, Secret Manager pour les clés API

→ [Rapport de gestion de projet complet dans ce repo](./rapport_gestion_projet_puls_events.pdf)

---

### Chatbot RAG — POC événements culturels Paris
`LangChain` `Mistral AI` `FAISS` `Python` `GitHub Actions` · *2026*

Point de départ de l'aventure Puls-Events. J'ai construit le premier prototype du chatbot de recommandation d'événements culturels sur les données Open Agenda (Grand Paris).

Pipeline complet : collecte de 300 événements via l'API avec pagination, prétraitement et filtrage géographique, indexation FAISS avec embeddings Mistral (1 024 dimensions), génération de réponses via LangChain. Tests unitaires et CI/CD GitHub Actions en place dès le départ.

Résultat : le POC a convaincu les équipes produit et marketing — c'est lui qui a lancé la phase MVP.

→ [github.com/dorrazch-hue/puls-events-rag](https://github.com/dorrazch-hue/puls-events-rag)

---

### BottleNeck — Pipeline de données automatisé
`Kestra` `PostgreSQL` `Python` `Docker` · *2026*

BottleNeck, marchand de vin, avait ses données dispersées entre un ERP et un site web, sans aucun process de consolidation. J'ai automatisé toute la chaîne avec Kestra : nettoyage SQL des trois sources, jointure, calcul du chiffre d'affaires par produit, puis détection des vins premium par score Z.

Le pipeline tourne en Docker Compose (Kestra + PostgreSQL) et livre chaque semaine un rapport Excel et deux fichiers CSV prêts à l'emploi. Zéro intervention manuelle.

→ [github.com/dorrazch-hue/bottleneck-data-pipeline](https://github.com/dorrazch-hue/bottleneck-data-pipeline)

---

### InduTech — Streaming temps réel de tickets clients
`Redpanda` `PySpark Structured Streaming` `Docker` `Python` · *Juillet 2026*

Pipeline de traitement de tickets clients en temps réel pour InduTech, entièrement conteneurisé. Le producteur Python génère un ticket par seconde sur un topic Redpanda (3 partitions, API Kafka). PySpark Structured Streaming consomme, enrichit chaque ticket (équipe support assignée, flag urgent) et sort les agrégations en temps réel en Parquet et JSON.

Projet réalisé et démontré en vidéo — de `docker compose up` jusqu'aux tableaux d'analyse en direct.

→ [github.com/dorrazch-hue/projet9-tickets-redpanda-pyspark](https://github.com/dorrazch-hue/projet9-tickets-redpanda-pyspark)

---

### GreenCoop — Pipeline ELT météo multi-stations
`Meltano` `AWS RDS` `PostgreSQL` `Python` · *Juillet 2026*

GreenCoop (Hauts-de-France) avait besoin de données de 6 stations météo semi-pro pour alimenter ses modèles de prévision de la demande électrique. Les données venaient de deux sources hétérogènes : l'API InfoClimat et des fichiers Excel Weather Underground.

J'ai construit un pipeline Meltano pour InfoClimat (période configurable via `.env`, sans dates en dur) et un script de chargement pour les fichiers Excel. Résultat : 9 463 observations nettoyées et dédupliquées, 14/14 tests de qualité passés, données déployées sur AWS RDS PostgreSQL (eu-west-3).

→ [github.com/dorrazch-hue/forecast2-greencoop](https://github.com/dorrazch-hue/forecast2-greencoop)

---

### Seattle Energy — API de prédiction déployée sur Cloud Run
`BentoML` `Google Cloud Run` `Python` `Jupyter` · *Juin 2026*

Modèle de prédiction de la consommation énergétique des bâtiments non-résidentiels de Seattle, packagé avec BentoML et déployé en production sur Google Cloud Run. L'API expose un endpoint POST `/predict` avec documentation Swagger auto-générée.

C'est l'un de mes premiers projets de ML en production — l'API est toujours accessible en ligne.

→ [github.com/dorrazch-hue/seattle-energy-api](https://github.com/dorrazch-hue/seattle-energy-api)

---

### DataSoluTech — Migration sécurisée de 55 500 dossiers médicaux
`MongoDB` `Docker` `Python` · *Mai 2026*

Migration de 55 500 dossiers médicaux vers une infrastructure MongoDB conteneurisée, avec sécurité pensée dès le départ : RBAC (4 rôles : root, admin, migrator, auditor), aucun secret en dur, traitement par chunks de 5 000 lignes pour ne pas exploser la RAM, réseau Docker isolé.

Un script `proof_security.py` démontre automatiquement que chaque rôle respecte bien ses permissions — les auditeurs ne peuvent pas écrire, les accès sans auth sont refusés.

→ [github.com/dorrazch-hue/projet-med-data](https://github.com/dorrazch-hue/projet-med-data)

---

## Stack

| | Technologies |
|---|---|
| **Langages** | Python 3.11, SQL |
| **NLP & IA** | LangChain, Mistral AI, Vertex AI (Gemini 1.5 Pro), Hugging Face smolagents, FAISS, ChromaDB |
| **Streaming** | Redpanda (API Kafka), PySpark Structured Streaming |
| **Pipelines** | Meltano, Kestra |
| **Bases de données** | PostgreSQL, MongoDB, Firestore |
| **Cloud** | GCP (Vertex AI, Cloud Run, Firestore), AWS (RDS) |
| **MLOps** | BentoML, Langfuse |
| **Infra** | Docker, Docker Compose, GitHub Actions |

---

**Dorra** · [github.com/dorrazch-hue](https://github.com/dorrazch-hue)
