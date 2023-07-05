## Helm installation

* Install Helm first. This of course depends on your OS. Check [Helm docs](https://helm.sh/docs/intro/install/) for more info.
* Check predefined [values](./keycloak-k8s-local/values.yaml) in the Helm package directory of this project. Change them according to your preferences.
* Before we try to install our chart let’s do a dry-run first, shall we? Just to see if everything’s OK.
```
helm template keycloak-k8s-local keycloak-k8s-local
```
If there is nothing for Helm to complain about the result will be a YAML file that contains all elements from separate YAMLs.

* Now it’s time to deploy the system! For this we invoke the install command by referencing the chart name and giving the name of the deployment.
  Install deployments with `helm install keycloak-k8s-local keycloak-k8s-local`

* Check current status with `watch -n 1 kubectl get all -n hbr-keycloak` 
* Uninstall with `helm uninstall keycloak-k8s-local`
