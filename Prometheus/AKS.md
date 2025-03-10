- Retrieve AKS Cluster Credentials for kubectl Access Locally

```
az aks get-credentials --resource-group <RESOURCE_GROUP> --name <AKS_CLUSTER_NAME>
```

- Install Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

- Add the Prometheus Helm Repo, which includes Prometheus, Alertmanager, and Grafana

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
```
helm repo update
```

- Deploy Prometheus using Helm

```
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace
```

- Check Prometheus is running

```
kubectl get pods -n monitoring
```

- Access Prometheus

```
kubectl port-forward -n monitoring svc/prometheus-kube-prometheus-prometheus 9090:9090
```

- Open your browser and navigate to

```
http://localhost:9090
```

- Grafana password

```
kubectl --namespace monitoring get secrets prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
```

- Grafana run locally with finding the pod name and export it

```
export POD_NAME=$(kubectl --namespace monitoring get pod -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=prometheus" -oname)
amespace monitoring port-forward $POD_NAME 3000
```

- Run Grafana on port 3000 using that pod name

```
kubectl --namespace monitoring port-forward $POD_NAME 3000
```

- Add the Loki repository

```
helm repo add grafana https://grafana.github.io/helm-cha
```
```
helm repo update
```

- Install the Loki stack

```
helm install loki-stack grafana/loki-stack --namespace monitoring --create-namespace
```

- Loki Port Forward

```
kubectl port-forward svc/loki-stack 3100:3100 -n monitoring
```


