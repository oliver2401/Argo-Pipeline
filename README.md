# Argo-Pipeline
main repo contianing master/root argo pipeline

## Prerequisites

before cloning/executing the repo verify that you have the following:

### Requirements
- Installed [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) command-line tool.
- Have a [kubeconfig](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) file (default location is `~/.kube/config`).
- CoreDNS. Can be enabled for `microk8s by microk8s enable dns && microk8s stop && microk8s start`

and then install Argo CD (stable version) via the following commands in the terminal:

### Install Argo CD

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Download Argo CD CLI
Install the stable CLI for Argo CD

```sh
VERSION=$(curl -L -s https://raw.githubusercontent.com/argoproj/argo-cd/stable/VERSION)
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/download/v$VERSION/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```


## ops-dev-app-deploy-pipeline

### Pre-requisites
#### ArgoCD[-SSO]
[ArgoCD-[SSO]] to be running.
Find reference in that repo on how-to install.

### Installing App of AppSets
```
git clone https://github.com/oliver2401/Argo-Pipeline.git

# Execute without --dry-run to actually install, otherwise test
helm upgrade --install root-app root-app -n argocd --set env="dev" --create-namespace \
    --set dags.gitSync.repo="" \
    --set dags.gitSync.branch="develop" \
    --dry-run
```

|helm --set override name|used by project|comments|
|------------------------|-------|--------|
|env|global|Actual environment to deploy to|
|dags.gitSync.repo|mlops||
|dags.gitSync.branch|mlops||