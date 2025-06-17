# Kubernetes Deployments

Este repositório contém arquivos de configuração para deploy da aplicação Iris completa usando Kubernetes, incluindo:

- **Frontend (React)** configurado com `ConfigMap`, `Deployment`, `Secret` e `Service`
- **Backend (API)** com `Deployment`, `Secret` e `Service`
- **PostgreSQL** com `Deployment`, `PersistentVolumeClaim`, `Secret`, `ConfigMap` e `Service`

## Estrutura do Projeto

```
kubernetes-deployments-main/
├── back/
│   ├── back-deployment.yaml
│   ├── back-secret.yaml
│   └── back-service.yaml
├── front/
│   ├── front-configmap.yaml
│   ├── front-deployment.yaml
│   ├── front-secret.yaml
│   └── front-service.yaml
├── postgres/
│   ├── postgres-configmap.yaml
│   ├── postgres-deployment.yaml
│   ├── postgres-pvc.yaml
│   ├── postgres-secret.yaml
│   └── postgres-service.yaml
```

## Pré-requisitos

- Cluster Kubernetes (Minikube, GKE, EKS, AKS etc.)
- `kubectl` instalado e configurado
- Namespace opcional (por padrão aplica-se no `default`)

## Como aplicar os arquivos

1. Clone este repositório:
```bash
git clone https://github.com/seu-usuario/kubernetes-deployments.git
cd kubernetes-deployments
```

2. Aplique os arquivos na seguinte ordem:

### PostgreSQL

```bash
kubectl apply -f postgres/postgres-secret.yaml
kubectl apply -f postgres/postgres-configmap.yaml
kubectl apply -f postgres/postgres-pvc.yaml
kubectl apply -f postgres/postgres-deployment.yaml
kubectl apply -f postgres/postgres-service.yaml
```

### Backend

```bash
kubectl apply -f back/back-secret.yaml
kubectl apply -f back/back-deployment.yaml
kubectl apply -f back/back-service.yaml
```

### Frontend

```bash
kubectl apply -f front/front-secret.yaml
kubectl apply -f front/front-configmap.yaml
kubectl apply -f front/front-deployment.yaml
kubectl apply -f front/front-service.yaml
```

## Observações

- Certifique-se de que os arquivos `Secret` e `ConfigMap` estejam corretamente configurados com suas credenciais e variáveis de ambiente.
- O volume persistente do PostgreSQL utiliza um `PersistentVolumeClaim`, podendo requerer configuração extra no cluster (ex: StorageClass).
