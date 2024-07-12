# KubeNodeApp Deployment on Google Cloud Kubernetes

This project demonstrates how to deploy a Node.js application on Google Cloud Kubernetes Engine (GKE) using Docker and Google Artifact Registry.

## Prerequisites

- Google Cloud account
- Google Cloud SDK installed
- Docker installed

## Steps to Build, Push, and Deploy

### Build and Push Docker Image

```bash
docker buildx create --use
docker buildx build --platform linux/arm64 -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/YOUR_REPO_NAME/kubenodeapp:latest .
docker buildx build --platform linux/amd64 -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/YOUR_REPO_NAME/kubenodeapp:latest --push .
```

### Create Namespace

```bash
kubectl apply -f namespace.yml
```

### Set image in the deployment.yml
```yaml
      containers:
        - name: kubenodeapp
          image: YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/YOUR_REPO_NAME/kubenodeapp:latest
          ports:
            - containerPort: 3000
```


### Deploy to Kubernetes
```bash
kubectl apply -f deployment.yml
kubectl apply -f service.yml
```

### Access the Application
```bash
kubectl get services -n kubenodeapp
```

## Troubleshooting

### Check Pod Logs

```bash
kubectl logs <pod-name> -n kubenodeapp
```

### Verify Image and Permissions:

```bash
gcloud auth configure-docker YOUR_REGION-docker.pkg.dev
```


