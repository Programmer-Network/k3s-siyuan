# K3s SiYuan Notes

This repository contains Kubernetes manifest files for deploying the [SiYuan note-taking application](https://github.com/siyuan-note/siyuan) on a K3S cluster using [ArgoCD](https://argo-cd.readthedocs.io/).

## Features

- **ArgoCD GitOps**: All manifests are designed to be managed via ArgoCD for a fully GitOps workflow.
- **Longhorn Storage**: StatefulSet uses Longhorn for persistent storage.
- **Traefik Ingress**: Ingress is configured for Traefik with TLS via cert-manager.
- **Namespace Isolation**: SiYuan runs in its own `siyuan` namespace.

## Usage

1. **Clone this repository**

```bash
git clone git@github.com:Programmer-Network/k3s-siyuan.git
cd k3s-siyuan
```

2. **Secret Management**

- **Do NOT commit real secrets to Git!**
- Use the provided `siyuan-secret.yaml` as a template:

- Replace `REPLACE_ME_BASE64` with your real base64-encoded auth code.
- Apply the secret manually:

```bash
kubectl apply -f siyuan-secret.yaml
```

3. **Deploy with ArgoCD**

- Add this repository to your ArgoCD instance as a new application.
- Sync the application to deploy all resources.
- Make sure the secret is created as described above.

## Notes

- All other resources (StatefulSet, Service, Ingress, etc.) are managed by ArgoCD.
- The SiYuan app will be available at the hostname configured in the ingress manifest.
- Persistent storage is provided by Longhorn; ensure Longhorn is installed in your cluster.
