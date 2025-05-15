# Argo CD Complete Setup Guide (Operator Method)

## 1. Prerequisites
- Kubernetes cluster (v1.16+)
- `kubectl` configured with cluster access
- Internet access from cluster

---

## 2. Install OLM (Operator Lifecycle Manager)
```bash
kubectl apply -f https://github.com/operator-framework/operator-lifecycle-manager/releases/latest/download/crds.yaml
kubectl apply -f https://github.com/operator-framework/operator-lifecycle-manager/releases/latest/download/olm.yaml

# Verify OLM installation
kubectl get pods -n olm --watch
## 
3. Create Namespaces

kubectl create namespace argocd-operator
kubectl create namespace argocd

4. Install Argo CD Operator

kubectl apply -f https://operatorhub.io/install/argocd-operator.yaml -n argocd-operator

# Verify operator installation
kubectl get pods -n argocd-operator -w


5. Deploy Argo CD Instance


6. Access Argo CD

# Get admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Port-forward service
kubectl port-forward svc/argocd-server -n argocd 8080:443

7. Connect Git Repository

argocd repo add https://github.com/Saisankar99-dev/Jenkins__ArgoCD.git \
  --name my-repo \
  --insecure-skip-server-verification
