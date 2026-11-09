# 👥 Gestion des Employés

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)

Application **full-stack** de gestion des employés (création, consultation, modification, suppression), entièrement **conteneurisée** et déployée en **mono-repo** grâce à un pipeline **CI/CD Jenkins**.

## 🏗️ Architecture

```
┌──────────────┐     HTTP/JSON     ┌──────────────┐     SQLAlchemy     ┌──────────────┐
│   Frontend   │ ────────────────▶ │   Backend    │ ─────────────────▶ │  PostgreSQL  │
│    React     │                   │   FastAPI    │                    │      17      │
│  (port 3000) │                   │  (port 8001) │                    │  (port 5432) │
└──────────────┘                   └──────────────┘                    └──────────────┘
                                                                              ▲
                                                                       ┌──────────────┐
                                                                       │   pgAdmin    │
                                                                       │  (port 8081) │
                                                                       └──────────────┘
```

## ✨ Fonctionnalités

- CRUD complet sur les employés (matricule, nom, poste, salaire)
- API REST documentée automatiquement par FastAPI (Swagger sur `/docs`)
- Interface React avec cartes employés et fenêtre modale d'édition
- Base PostgreSQL avec healthcheck et administration via pgAdmin
- Pipeline Jenkins : build des images, push sur Docker Hub, déploiement

## 🔌 Endpoints de l'API

| Méthode | Route | Description |
|---|---|---|
| `POST` | `/api/employes/` | Créer un employé |
| `GET` | `/api/employes/` | Lister les employés |
| `GET` | `/api/employes/{id}` | Détail d'un employé |
| `PUT` | `/api/employes/{id}` | Modifier un employé |
| `DELETE` | `/api/employes/{id}` | Supprimer un employé |

## 🚀 Lancer le projet

```bash
git clone https://github.com/kalpafall/gestion-employe.git
cd gestion-employe
docker compose up -d --build
```

| Service | URL |
|---|---|
| Frontend | http://localhost:3000 |
| API (Swagger) | http://localhost:8001/docs |
| pgAdmin | http://localhost:8081 |

## 🔄 Pipeline CI/CD (Jenkins)

1. **Checkout** du code
2. **Build** des images Docker backend et frontend
3. **Push** des images versionnées sur Docker Hub
4. **Déploiement** de la stack avec Docker Compose

## 📁 Structure

```
gestion-employe/
├── backend/            # API FastAPI (models, schemas, crud, database)
├── frontend/           # Application React
├── docker-compose.yaml # Orchestration des services
└── Jenkinsfile         # Pipeline CI/CD
```

---

Projet réalisé en équipe, à partir du dépôt [fatydiengmsf-dotcom/gestion-employe](https://github.com/fatydiengmsf-dotcom/gestion-employe).
