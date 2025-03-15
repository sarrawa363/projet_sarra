# Backend API avec MySQL

Ce projet fournit une API RESTful simple avec Node.js et Express qui se connecte à MySQL. L'application complète est conteneurisée et peut être déployée à l'aide de Docker et Kubernetes.

## Points de terminaison API

- `GET /api/items`: Récupérer tous les éléments
- `POST /api/items`: Créer un nouvel élément

## Prérequis

- Docker et Docker Compose
- Cluster Kubernetes (pour le déploiement K8s)
- CLI kubectl

## Exécution locale avec Docker Compose

1. Clonez ce dépôt
2. Remplacez `sarrawa363` dans docker-compose.yaml par votre ID Docker Hub
3. Construisez et démarrez les conteneurs:

```bash
docker-compose up -d
```

4. L'API sera disponible à l'adresse http://localhost:3000

## Construction et envoi de l'image Docker

```bash
# Construire l'image
docker build -t sarrawa363/backend:v1.0.0 .

# Envoyer vers Docker Hub
docker login
docker push sarrawa363/backend:v1.0.0
```

## Déploiement sur Kubernetes

1. Remplacez `sarrawa363` dans `kubernetes/backend-deployment.yaml` par votre ID Docker Hub
2. Appliquez tous les manifestes Kubernetes:

```bash
kubectl apply -f kubernetes/
```

3. Pour accéder au service:

```bash
# Pour les tests/développement, vous pouvez utiliser le port-forwarding
kubectl port-forward service/backend-service 8080:80
```

Ensuite, accédez à l'API à l'adresse http://localhost:8080

## Test de l'API

Vous pouvez tester l'API à l'aide de curl:

```bash
# Obtenir tous les éléments
curl http://localhost:3000/api/items

# Créer un nouvel élément
curl -X POST -H "Content-Type: application/json" -d '{"name":"Élément de test","description":"Ceci est un élément de test"}' http://localhost:3000/api/items
```

## Structure du projet

.```
├── node_modules               
├── app.js                     
├── package.json               
├── Dockerfile                 
├── docker-compose.yaml        
├── kubernetes/
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── mysql-pvc.yaml
│   └── mysql-secret.yaml
└── README.md                  # Ce fichier
```

## Remarques
- Pour une utilisation en production, vous devriez ajuster les ressources allouées dans les fichiers de déploiement Kubernetes.