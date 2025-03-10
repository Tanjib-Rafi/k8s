### Attach an Azure Container Registry (ACR) to an Azure Kubernetes Service (AKS) cluster

### Method 1: 

- Get ACR Login Credentials :

```
az acr credential show --name registry-name
```

- Enable admin access if not enabled :

```
az acr update --name registry-name --admin-enabled true
```

- Create K8s secret for docker registry:

```
kubectl create secret docker-registry registry-name --docker-server=registry-name.azurecr.io --docker-username= --docker-password= --docker-email=
```

### Method 2:

- Get the name of your AKS cluster and resource group

```
AKS_NAME=cluster_name
```


```
RESOURCE_GROUP=<your-resource-group>
```


```
ACR_NAME=acr_name
```

- Attach the ACR to your AKS cluster:

```
az aks update --name $AKS_NAME --resource-group $RESOURCE_GROUP --attach-acr $ACR_NAME
```


### Commands for ACR

```
az acr login --name acr_name
```

> subscription list

```
az account list --output table
```

```
az account set --subscription subscription_id
```

```
az acr credential show --name registry_name
```

> login server of acr

```
az acr list --output table
```

> build docker image

```
docker build -t acr_name.azurecr.io/image_name:latest .
```

```
docker login acr_name.azurecr.io -u 00000000-0000-0000-0000-000000000000 -p <accessToken>
```

> docker push image
```
docker push acr_name.azurecr.io/image_name:latest
```

```
az acr repository list --name acr_name --output table
```


> ACR Admin Credentials (username and password)


```
az acr update --name <acr-name> --admin-enabled true
```

```
az acr credential show --name <acr-name> --query "{username:username, password:passwords[0].value}" --output json
```


### Commands for AKS

```
az aks get-credentials --resource-group <your-resource-group> --name <your-aks-cluster-name>
```


### Locally install az bash | set kubectl config

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```


```
az login
```


```
az aks get-credentials --resource-group <resource-group-name> --name <aks-cluster-name>
```


```
kubectl config current-context
```


```
kubectl get nodes
```


### Github Actions
> A service principal (SP) is essentially an identity used by applications, services, or automation tools (like GitHub Actions) to authenticate and perform actions in Azure. It allows you to control the permissions of the application (e.g., allowing it to deploy to your AKS cluster)

AZURE_TENANT_ID:
```
az account show --query tenantId
```

Find the subscription id:
```
az account list --output table
```

Create a service principal and get credentials:
```
az ad sp create-for-rbac --name "my-github-action-sp" --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

```
az ad sp create-for-rbac --name github-actions-sp --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} --sdk-auth
```


