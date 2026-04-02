# FluxCD Setup

This directory contains the FluxCD configuration for the `portfolio` application.

## Structure
- `apps/portfolio.yaml`: Defines the `GitRepository` and `Kustomization` (app source and deployment sync).

## How to reconcile

1.  **Install Flux CLI** (if not already):
    ```bash
    curl -s https://fluxcd.io/install.sh | sudo bash
    ```

2.  **Bootstrap Flux (Recommended)**:
    If flux is NOT yet on your k3d cluster, run:
    ```bash
    flux bootstrap github \
      --owner=a-nasruddin \
      --repository=k8s-manifest \
      --branch=main \
      --path=./fluxcd/clusters/my-cluster \
      --personal
    ```

3.  **Manual Application**:
    If you just want to apply these configs manually to an existing Flux installation:
    ```bash
    kubectl apply -f fluxcd/apps/portfolio.yaml
    ```

## Reconciliation
Flux will check the Git repository every minute for changes and update the cluster automatically.
To force a sync:
```bash
flux reconcile kustomization portfolio-kustomization --with-source
```
