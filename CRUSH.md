## Getting Started

This is a GitOps repository for a Kubernetes homelab, managed by ArgoCD.

### Installation

1.  **Clone the repository:**
    `git clone https://github.com/bernylinville/k3s-argocd-homelab.git`
2.  **Install prerequisites:**
    - A running K3s cluster
    - `kubectl` configured to connect to your cluster
    - `helm` v3+
    - `argocd` CLI

### Bootstrapping the Environment

The core of this setup is ArgoCD. To bootstrap the environment, you'll need to install the ArgoCD controller in your cluster and then apply the main application set, which manages all other applications.

`kubectl apply -f infrastructure/controllers/argocd/projects.yaml`

This will create the initial ArgoCD projects. From there, ArgoCD will pick up the applications defined in the `my-apps` and `monitoring` directories.

## Development Workflow

All changes to the cluster are made through Git. Modify the Kubernetes manifests or Helm values in this repository, and ArgoCD will automatically sync the changes to your cluster.

### Linting and Validation

Since this project primarily uses YAML, there isn't a traditional build or test step. Instead, focus on validating your Kubernetes manifests.

- **YAML Linting:** Use a tool like `yamllint`.
  `yamllint .`

- **Kubernetes Manifest Validation:** Use `kubeval` or `kubectl --dry-run=server`.
  `find . -name "*.yaml" -exec kubectl --dry-run=server -f {} \;`

### Code Style and Conventions

- **YAML:**
    - Indentation: 2 spaces.
    - Use comments to explain non-obvious configurations.
- **Helm:**
    - Follow Helm best practices for chart structure.
    - Keep `values.yaml` well-documented.
- **ArgoCD:**
    - Use ApplicationSets for managing groups of applications.
    - Keep applications organized by function (e.g., `monitoring`, `my-apps`).
- **Commits:**
    - Use conventional commit messages (e.g., `feat: add new application`, `fix: correct service port`).
