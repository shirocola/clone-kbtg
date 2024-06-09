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