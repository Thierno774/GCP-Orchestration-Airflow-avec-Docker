# Orchestration Airflow sur GCP avec Docker

---

## 1️⃣ Introduction

Ce projet illustre la mise en place d’un environnement **Airflow** orchestré via **Docker Compose** sur une **VM Google Compute Engine**.  
Il permet de gérer des **DAGs** pour l’ingestion, le traitement et le reporting de données, tout en intégrant un **workflow CI/CD** pour déploiement automatisé.

**Technologies utilisées :**  
- **Google Cloud Platform (GCP)** : Compute Engine, VPC, Firewall, PostgreSQL  
- **Docker & Docker Compose** : Conteneurisation de Airflow  
- **Git & GitHub** : Versioning et CI/CD  
- **Python & Airflow** : Orchestration des tâches  

---

## 2️⃣ Architecture

Le schéma ci-dessous montre l’architecture complète du projet, incluant la VM, Docker Compose, Airflow Scheduler, Webserver, Postgres et les dossiers DAGs / Logs / Plugins.

![Architecture Airflow Docker GCP](/pipelines_airflow.png)  

*Auteur : Thierno BAH*

---

## 3️⃣ Prérequis

- Compte Google Cloud Platform avec projet actif  
- VM Compute Engine sous Ubuntu 22.04  
- Docker et Docker Compose installés  
- Git et GitHub configurés  
- Ports HTTP/HTTPS ouverts pour accéder à Airflow Web UI (8080)

---

## 4️⃣ Configuration de la VM GCP

1. **Créer une VM Compute Engine** :
   - Ubuntu 22.04 LTS Minimal  
   - SSD 20 GB  
   - Ouvrir HTTP/HTTPS et port TCP 8080 via Firewall  

2. **Configurer le réseau VPC** et les autorisations nécessaires pour la VM.  

3. **Créer un compte de service** avec permissions :
   - `roles/editor` pour le projet (ou permissions spécifiques pour Airflow et Docker)  
   - Accès à Cloud Storage et PostgreSQL  

---

## 5️⃣ Installation d’Airflow avec Docker Compose

1. Cloner le projet :
```bash
git clone https://github.com/ton-utilisateur/nom-du-repo.git
cd nom-du-repo/airflow-docker
```

2. Créer les dossiers Airflow :
```bash
mkdir -p dags logs plugins
```

3. Initialiser Docker Compose :
```bash
docker-compose up -d
```

4. Initialiser la base de données Airflow :
```bash
docker-compose run --rm airflow-webserver airflow db init
```

5. Démarrer Airflow Scheduler et Webserver :
```bash
docker-compose up -d airflow-scheduler
docker-compose up -d airflow-webserver
```

6. Accéder à l’UI Airflow :  
`http://<IP_VM>:8080`  

---

## 6️⃣ Git & GitHub Workflow

1. Initialiser le dépôt local :
```bash
git init
```

2. Ajouter les fichiers :
```bash
git add .
```

3. Commit avec un message clair :
```bash
git commit -m "Initial commit Airflow Docker GCP"
```

4. Ajouter le dépôt distant :
```bash
git remote add origin https://github.com/ton-utilisateur/nom-du-repo.git
```

5. Envoyer les commits sur GitHub :
```bash
git push -u origin main
```

6. Pour les modifications futures :
```bash
git add .
git commit -m "Message descriptif"
git push
```

---

## 7️⃣ CI/CD (optionnel)

- Un trigger Cloud Build peut être configuré pour builder et déployer automatiquement vos DAGs Airflow dans le conteneur Docker sur la VM à chaque push sur `main`.  
- Permet un **déploiement continu** et versionné de votre orchestration.

---

## 8️⃣ Structure du projet

```
airflow-docker/
├─ dags/             # DAGs Airflow
├─ logs/             # Logs des exécutions
├─ plugins/          # Plugins personnalisés
├─ docker-compose.yml
├─ Dockerfile        # si nécessaire pour custom images
└─ README.md
```

---

## 9️⃣ Auteurs & Contributions

- **Thierno BAH** – Auteur et mainteneur du projet  
- Contributions possibles via pull request sur GitHub  

---

## 🔗 Ressources utiles

- [Documentation Airflow](https://airflow.apache.org/docs/)  
- [Docker Compose](https://docs.docker.com/compose/)  
- [Google Compute Engine](https://cloud.google.com/compute)  
- [CI/CD avec Cloud Build](https://cloud.google.com/build)

