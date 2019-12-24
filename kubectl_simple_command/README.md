# dec_kubectl_stage

Simple solution not using plugins

* Create kubeconfig and add as a secret

## Creating kubeconfig
### GKE
https://gravitational.com/blog/kubectl-gke/

```
gcloud container clusters get-credentials <cluster-name> --project <project-name>
```

Request a new certificate, good example below

```
https://github.com/gravitational/teleport/blob/master/examples/gke-auth/get-kubeconfig.sh
```

kubeconfig file is created in the deploy directory

### EKS
Creat a service principal

```
az ad sp create-for-rbac -n "MyJenkinsApp" --create-cert
```

```
az login --service-principal --username http://MyJenkinsApp --password <path to cert displayed from output of previous command> --tenant <displayed from output of previous command> 
```