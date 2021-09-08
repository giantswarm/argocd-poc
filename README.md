# argocd-poc

POC to install argocd on Workload clusters.


## Layout

- AppProject: `argocd` contains:
  - Application: `argocd` manages itself:
    -  upstream Argo CD manifests
    - `argocd` AppProject CR
    - `argocd` Application CR

## Updating Argo CD manifests

Run

```
make all
```

This make target will:
  - update `manifests/bases/upstream-argocd/` with version of ArgoCD specified in Makefile.
  - render `bootstrap/argocd.yaml` file with the project for self-managed provider application.

Those directories' content can be rendered separately using different make targets:
  - `make manifests/bases/upstream-argocd` - updates upstream ArgoCD.
  - `make bootstrap` - updates `bootstrap/` resources.

To change the version of rendered manifests, update `ARGOCD_VERSION` in [Makefile.custom.mk](Makefile.custom.mk).
You might have to change image override in `manifests/argocd/kustomization.yaml` as well.