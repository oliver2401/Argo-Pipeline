# Argo-Pipeline
main repo contianing master/root argo pipeline


## ops-dev-app-deploy-pipeline

### Pre-requisites
#### ArgoCD[-SSO]
[ArgoCD-[SSO]] to be running.
Find reference in that repo on how-to install.

### Installing App of AppSets
```
git clone <repo_TBD>

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