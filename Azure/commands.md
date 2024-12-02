### Attach an Azure Container Registry (ACR) to an Azure Kubernetes Service (AKS) cluster

### Method 1: 

- Get ACR Login Credentials :

```az acr credential show --name registry-name```

- Enable admin access if not enabled :

```az acr update --name registry-name --admin-enabled true```

- Create K8s secret for docker registry:

```kubectl create secret docker-registry registry-name --docker-server=registry-name.azurecr.io --docker-username= --docker-password= --docker-email=```

### Method 2:

- Get the name of your AKS cluster and resource group

```AKS_NAME=cluster_name```

```RESOURCE_GROUP=<your-resource-group>```

```ACR_NAME=acr_name```

- Attach the ACR to your AKS cluster:

```az aks update --name $AKS_NAME --resource-group $RESOURCE_GROUP --attach-acr $ACR_NAME```


### Commands

```az acr login --name acr_name```

```az acr credential show --name registry_name```

```docker build -t acr_name.azurecr.io/image_name:latest .```

```docker push acr_name.azurecr.io/image_name:latest```

```