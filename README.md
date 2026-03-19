# 🚀 Node.js DevSecOps Monitoring

## 📌 Description

Ce projet met en place une application **Node.js instrumentée**, intégrée dans une démarche **DevSecOps complète** incluant :

- CI/CD avec GitHub Actions
- Analyse de sécurité (Trivy, CodeQL, Hadolint)
- Conteneurisation Docker
- Monitoring avec Prometheus & Grafana

L’objectif est de démontrer la mise en œuvre d’une pipeline sécurisée et d’un système de supervision en temps réel.

---

## 🏗️ Architecture

```
Développeur → GitHub → CI/CD (GitHub Actions)
                             ↓
                    Build / Scan / Analyse
                             ↓
                    Image Docker (GHCR)
                             ↓
                  Docker Compose (local)
                             ↓
        App Node.js → Prometheus → Grafana
```

---

## ⚙️ Stack technique

### Backend
- Node.js (Express)
- prom-client (métriques Prometheus)

### DevOps / Sécurité
- Docker
- GitHub Actions
- Trivy (scan vulnérabilités)
- Hadolint (lint Dockerfile)
- CodeQL (analyse statique)

### Monitoring
- Prometheus
- Grafana
- Node Exporter

---

## 🚀 Lancer le projet

### 1. Cloner le repository

```bash
git clone https://github.com/ghosted123-sudo/nodeapp-devsecops.git
cd nodeapp-devsecops
```

### 2. Lancer la stack complète

```bash
docker compose up -d --build
```

### 3. Vérifier les conteneurs

```bash
docker compose ps
```

---

## 🌐 Accès aux services

| Service        | URL                          | Identifiants     |
|----------------|-----------------------------|------------------|
| Application    | http://localhost:3000       | —                |
| Metrics        | http://localhost:3000/metrics | —              |
| Prometheus     | http://localhost:9090       | —                |
| Grafana        | http://localhost:3001       | admin / admin123 |

---

## 📊 Monitoring

### Prometheus
- Scraping toutes les 15 secondes
- Cibles :
  - `app:3000`
  - `node-exporter:9100`

### Grafana Dashboard

Le dashboard inclut :

- 📈 Requêtes par seconde
- ⚠️ Taux d’erreur (%)
- ⏱️ Latence p95 (ms)

---

## 🧪 Générer du trafic

```bash
for i in $(seq 1 100); do
  curl -s http://localhost:3000/ > /dev/null
  curl -s http://localhost:3000/health > /dev/null
  sleep 0.2
done
```

### Générer des erreurs

```bash
for i in $(seq 1 50); do
  curl -s http://localhost:3000/error > /dev/null
  sleep 0.2
done
```

---

## 🔐 Pipeline DevSecOps

Le pipeline GitHub Actions comprend :

1. Build & Test
   - Installation des dépendances
   - Vérification du démarrage de l’application

2. Lint Dockerfile
   - Analyse avec Hadolint

3. Scan de sécurité
   - Trivy (vulnérabilités image Docker)

4. Analyse statique
   - CodeQL (JavaScript)

5. Publication
   - Push de l’image sur GitHub Container Registry (GHCR)

---

## 🛡️ Sécurité

- Utilisateur non-root dans Docker
- Scan automatique des vulnérabilités
- Blocage des builds en cas de vulnérabilités critiques
- Dépendances auditées avec `npm audit`

---

## 📁 Structure du projet

```
nodeapp-devsecops/
├── .github/workflows/devsecops.yml
├── prometheus/prometheus.yml
├── app.js
├── package.json
├── Dockerfile
├── docker-compose.yml
└── .dockerignore
```

---

## 🧠 Concepts clés

- DevSecOps : intégration de la sécurité dans le pipeline CI/CD
- Observabilité : collecte et visualisation des métriques applicatives
- Containerisation : isolation et déploiement via Docker
- Monitoring temps réel : Prometheus + Grafana

---

## 🏁 Conclusion

Ce projet démontre la mise en place d’un environnement complet combinant :

- développement applicatif
- sécurité automatisée
- déploiement conteneurisé
- supervision en temps réel

Il constitue une base solide pour des architectures DevSecOps modernes.

---

## 👤 Auteur

- GitHub : https://github.com/ghosted123-sudo
