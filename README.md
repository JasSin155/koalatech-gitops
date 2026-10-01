# koalatech-gitops

Desired state of the KoalaTech Course Platform `production` namespace, reconciled by Argo CD. SIT722 Task 10.3HD, paired with [koalatech-hd](https://github.com/JasSin155/koalatech-hd).

* `manifests/` is rendered with kustomize. Five PostgreSQL databases, five FastAPI services, the frontend, the `koalatech-sa` ServiceAccount (Workload Identity) and the `SecretProviderClass` that mounts Key Vault secrets.
* `argocd/koalatech-production.yaml` is the Argo CD Application, applied once. Automated sync with `prune` and `selfHeal`.

There are no secrets in this repository. The only values that differ per environment are identifiers (managed identity client id, tenant id, vault name, registry name).

The only automated writer is the koalatech-hd CI pipeline, which changes the `images:` block of `manifests/kustomization.yaml` after an image has passed both security gates. Any other change is made by a human commit, and Argo CD applies it within about three minutes.
