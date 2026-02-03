
## A Complete Application Lifecycle: Ecommerce

The assignment demonstrates deploying a microservices-based ecommerce application on Kubernetes using AWS EKS, Kubernetes manifests, and Helm for release management.

### Architecture Summary

Request flow:

Frontend → API Gateway → Backend Services

* Frontend and API Gateway are exposed using AWS LoadBalancer services
* Product and Order services use ClusterIP for internal communication
* Blue-Green and Canary deployment strategies are demonstrated
* Helm is used for upgrades and rollbacks
``
## Deployment

```
### Cluster Creation
```bash
eksctl create cluster --name ecommerce-cluster --region us-east-1
```

### Deploy Manifests

```bash
kubectl apply -f manifests/
```

### Helm Operations

Install:

```bash
helm install product helm/ecommerce -n ecommerce
```

Upgrade:

```bash
helm upgrade product helm/ecommerce --set replicaCount=3 -n ecommerce
```

Rollback:

```bash
helm rollback product <revision> -n ecommerce
```

---

## Demo Verification

* Pods verified using `kubectl get pods`
* Services verified using `kubectl get svc`
* Scaling verified by increasing replica count
* Rollback verified by restoring previous replica count

---

## Cleanup

```bash
helm uninstall product -n ecommerce
eksctl delete cluster --name ecommerce-cluster --region us-east-1
```
