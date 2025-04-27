
This repository implements a GitOps workflow for deploying multiple microservices using ArgoCD and Helm. Each microservice has its own Helm chart, and environment-specific values are managed separately for easy promotion and configuration.

## Structure

```
app-gitops/
├── apps/
│   ├── microservice1/
│   ├── microservice2/
│   └── microservice3/
├── environments/
│   ├── dev/
│   ├── test/
│   └── prod/
└── applicationset/
    └── microservices-appset.yaml
```

- **apps/**: Contains a Helm chart for each microservice.
- **environments/**: Contains environment-specific values files for each microservice.
- **applicatioset/**: Contains the ArgoCD ApplicationSet manifest to automate deployment of all microservices across environments.

## How it works

- Each microservice is defined as a Helm chart under `apps/`.
- For each environment (`dev`, `test`, `prod`), there are values files that override the default Helm values for each microservice.
- The `microservices-appset.yaml` uses ArgoCD ApplicationSet to automatically create ArgoCD Applications for each microservice and environment.

## Usage

1. **Clone the repository**  
   ```sh
   git clone <repo-url>
   cd app-gitops-digital-platform
   ```

2. **Configure your ArgoCD instance**  
   - Point ArgoCD to this repository.
   - Apply the ApplicationSet manifest:
     ```sh
     kubectl apply -f applicationset/microservices-appset.yaml
     ```

3. **Update microservices or environment values**  
   - Edit the Helm charts in `apps/` or the values files in `environments/`.
   - Commit and push changes. ArgoCD will automatically sync and deploy updates.

## Adding a New Microservice

1. Create a new Helm chart under `apps/`.
2. Add environment-specific values files under each environment in `environments/`.
3. No need to update the ApplicationSet if using the directory generator.

## Requirements

- [ArgoCD](https://argo-cd.readthedocs.io/)
- [Helm](https://helm.sh/)
- Kubernetes cluster
