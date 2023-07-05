## Keycloak with PostgreSQL on Kubernetes (KinD)

### Dependencies

- [Docker](https://docs.docker.com/engine/install/ubuntu/)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)

### KinD

```
$ cd kind
### Create k8s Cluster 
$ kind create cluster --name=hbr-cluster --config=config.yml

### Install NGINX Ingress
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

### Manual installation

To install everything by hand, use the YAMLs located [here](./deployments/manual/README.md).

### Helm installation

For Helm installation go [here](./deployments/helm/README.md).

### REF: https://github.com/brakmic/Keycloak_on_Kubernetes
