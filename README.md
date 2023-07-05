## Keycloak with PostgreSQL on Kubernetes (KinD)

### Dependencies

- [Docker](https://docs.docker.com/engine/install/ubuntu/)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)

### k8s setup (KinD)

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

### Checks
```
$ kubectl get po -n hbr-keycloak
NAMESPACE            NAME                                                READY   STATUS      RESTARTS   AGE
hbr-keycloak         keycloak-6665dd859-6kntt                            1/1     Running     0          6m1s
hbr-keycloak         postgres-6b64958df7-szjq9                           1/1     Running     0          46m

$ kubectl exec -it postgres-6b64958df7-szjq9 -n hbr-keycloak -- psql -h localhost -U postgres --password -p 5432 keycloak
Password: aab++112
psql (15.3 (Debian 15.3-1.pgdg120+1))
Type "help" for help.

keycloak=# \l
                                                List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    | ICU Locale | Locale Provider |   Access privileges   
-----------+----------+----------+------------+------------+------------+-----------------+-----------------------
 keycloak  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | 
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | =c/postgres          +
           |          |          |            |            |            |                 | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | =c/postgres          +
           |          |          |            |            |            |                 | postgres=CTc/postgres
(4 rows)

keycloak=# exit

$ kubectl get ing --all-namespaces
NAMESPACE      NAME       CLASS    HOSTS       ADDRESS     PORTS     AGE
hbr-keycloak   keycloak   <none>   localhost   localhost   80, 443   58s
```

Access Keycloak UI (Browser): https://localhost/admin/master/console/

<img src="images/keycloak-UI.png?raw=true" width="1000">


### [Thanks]( https://github.com/brakmic/Keycloak_on_Kubernetes)
