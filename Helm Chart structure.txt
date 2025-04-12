---
# 🌟 Helm Chart Directory Structure
# ./helm-chart/
# ├── Chart.yaml
# ├── values.yaml
# ├── templates/
# │   ├── deployment.yaml
# │   ├── service.yaml
# │   ├── ingress.yaml

# 📁 Chart.yaml
apiVersion: v2
name: myapp
version: 1.0.0
description: A sample Helm chart for backend/frontend

---
# 📁 values.yaml (Dev Example)
replicaCount: 1
image:
  repository: pravindevops/backend
  tag: "latest"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 8080

ingress:
  enabled: false

resources: {}

---
# 📁 templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Chart.Name }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Chart.Name }}
  template:
    metadata:
      labels:
        app: {{ .Chart.Name }}
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          ports:
            - containerPort: {{ .Values.service.port }}

---
# 📁 templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ .Chart.Name }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app: {{ .Chart.Name }}
  ports:
    - protocol: TCP
      port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}

---
# 📁 .github/workflows/deploy.yml
name: CI/CD Pipeline

on:
  push:
    branches:
      - dev
      - main

jobs:
  build-and-push:
    name: Build & Push Docker Image
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and Push Image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: pravindevops/backend:${{ github.sha }}

  deploy:
    name: Deploy to Kubernetes
    needs: build-and-push
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Kubeconfig
        uses: azure/setup-kubectl@v3
        with:
          version: 'v1.26.0'

      - name: Deploy with Helm
        run: |
          helm upgrade --install myapp ./helm-chart \
            --set image.tag=${{ github.sha }} \
            --namespace dev
        env:
          KUBECONFIG: ${{ secrets.KUBECONFIG }}
