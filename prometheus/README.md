
Run a Kubernetes cluster then the following commands to:
    create a namespace, config-mapping, role, services and deploy.

```
kubectl apply -f namespace.yml
kubectl apply -f config-map.yml
kubectl apply -f rbac.yml
kubectl apply -f deployment.yml
kubectl apply -f node-service.yml

```
Open URL
```
minikube service list
```

Enter ```{job=”prometheus”}``` to access available metrics.

```
kubectl apply -f node-exporter-daemonset.yml
```

Clean-up

```kubectl delete namespace monitoring```