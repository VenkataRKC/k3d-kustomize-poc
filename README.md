# k3d + Kustomize + ArgoCD POC

Frontend/backend demo using `stefanprodan/podinfo` with dev and prod overlays.

## Quick Reference

| Environment | Frontend Color | Backend Color | Image Tag | Replicas |
|---|---|---|---|---|
| dev | Blue `#34577c` | Green `#2e7d32` | 6.5.0 | 1/1 |
| prod | Pink `#e91e63` | Orange `#f57c00` | 6.7.0 | 3/2 |

## Repo Structure

```
.
├── apps/
│   ├── base/
│   │   ├── frontend/       # Shared base manifests
│   │   └── backend/
│   └── overlays/
│       ├── dev/            # Dev-specific patches
│       └── prod/           # Prod-specific patches
└── argocd/
    ├── app-dev.yaml        # ArgoCD Application for dev
    └── app-prod.yaml       # ArgoCD Application for prod
```

## Validate Kustomize Locally

```bash
kustomize build apps/overlays/dev
kustomize build apps/overlays/prod
```

## Useful Commands

```bash
# Watch pods
kubectl get pods -n dev -w
kubectl get pods -n prod -w

# Port forward to test
kubectl port-forward svc/dev-frontend -n dev 8081:9898
kubectl port-forward svc/dev-backend  -n dev 8082:9898
kubectl port-forward svc/prod-frontend -n prod 8083:9898

# ArgoCD
argocd app list
argocd app sync poc-dev
argocd app sync poc-prod
```
