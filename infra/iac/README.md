# Terraform for K8s
- Create cluster
- Create VPC, Subnet, Route Table, Internet Gateway, Nat Gateway
- Install ArgoCD
- Install Nginx Ingress Controller
- Mapping DNS to ArgoCD (Cloudflare)


## K8s Credential

```sh
aws eks update-kubeconfig --name <CLUSTER_NAME>

aws eks update-kubeconfig --name eks-clone-workshop
```

## Ingress Controller
-Enable `ssl-passthrough` via `'--enable-ssl-passthrough'` flag

```sh
kubectl -n ingress-nignx edit deployment. apps/ingress-nginx-controller
```

## Secret from ArgoCD

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo 
```

## ArgoCD Users
```sh

# creat configmap file from argocd-cm
kubectl get configmap argocd-cm -n argocd -o yaml > argocd-cm.yml

# edit argocd-cm.yml
data:
 accounts.<ACCOUNT_NAME>: apiKey, login

# apply configmap
kubectl apply -f argocd-cm.yml -n argocd

# Set RBAC for the user
kubectl get configmap argocd-rbac-cm -n argocd -o yaml > argocd-rbac-cm.yml

# edit argocd-rbac-cm.yml
data:
 policy.csv: |
   g, <ACCOUNT_NAME>, role:admin

# apply configmap rbac
kubectl apply -f argocd-rbac-cm.yml -n argocd