# homelab-k8s-test

This is a minimal test repository for testing the homelab bootstrap functionality. It contains only the essential structure needed to validate the bootstrap process works correctly without any production dependencies.

## Structure

```
├── clusters/kind/flux/          # Flux configuration for Kind environment
│   ├── flux-system/            # Core Flux system resources
│   ├── infrastructure.yaml     # Points to infrastructure layer
│   └── apps.yaml              # Points to application layer
├── infrastructure/             # Infrastructure layer
│   ├── base/                  # Base infrastructure resources
│   └── kind/                  # Kind-specific overrides
├── apps/                      # Application layer
│   ├── base/                  # Base application definitions
│   └── kind/                  # Kind-specific overrides
├── Taskfile.yml              # Basic validation tasks
└── .sops.yaml                # SOPS configuration for testing
```

## Purpose

This repository is designed to test:

1. **Infrastructure Bootstrap** - Validates that the bootstrap process can:
   - Install Flux runtime components
   - Create necessary secrets (SOPS, Git deploy keys)
   - Set up the GitOps foundation

2. **Kustomization Validation** - Ensures all kustomizations build correctly:
   - Infrastructure layer (base + kind overlay)
   - Application layer (base + kind overlay)
   - Flux system configuration

3. **End-to-End Testing** - Provides a realistic but minimal GitOps structure for testing the complete bootstrap pipeline on Kind clusters

## Usage

### Validate Structure
```bash
task validate
```

### Test Kustomization Builds
```bash
task kustomize-build-all
```

## Testing with Bootstrap

This repository is used by the main homelab-k8s repository's E2E tests:

```bash
# In the main homelab-k8s repository
task test:e2e:bootstrap
```

The tests use `SkipGitBootstrap=true` to focus on infrastructure validation while using this repository's structure for GitOps layout validation.

## Components

- **Flux System**: Minimal Flux configuration for Kind clusters
- **Test Infrastructure**: Simple namespace and ConfigMap for validation
- **Test Application**: Lightweight nginx deployment for application layer testing
- **Environment Overrides**: Kind-specific patches and configurations

This structure mirrors the production homelab repository but with minimal, test-focused resources instead of real infrastructure components.




## Run

from: https://github.com/erauner/homelab-k8s


ssh key:
```
eval $(ssh-agent -s) && ssh-add ~/.ssh/id_ed25519 && SSH_AUTH_SOCK=$SSH_AUTH_SOCK SSH_AGENT_PID=$SSH_AGENT_PID task test:e2e:bootstrap
```

deploy key:

```
TBD
```
