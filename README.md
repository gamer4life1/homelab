# Heqet Apps

This is an example / boilerplate for your [heqet](https://lib42.github.io/heqet) configuration.

## Bootstrap Argo-CD + Heqet

###  1. Install Argo-CD with heqet-CMP
``` shellsession
helm repo add argo https://argoproj.github.io/argo-helm
helm install --create-namespace -f projects/argocd/values/argocd.yaml -n argocd argocd argo/argo-cd 
```

### 2. Push your configuration to git repo

### 3. Bootstrap Heqet

After adding your git-repo url:
``` shellsession
kubectl apply -f bootstrap.yaml
```

## Install Heqet CLI [Optional]
``` shellsession
helm plugin install https://github.com/lib42/helm-heqet.git
```

## Repo Structure

```
├── bootstrap.yaml            # Used for initial bootstrap of Heqet
├── Heqetfile                 # Required for Heqet to work
├── projects/
│   └── argocd/               # Every project has it's own folder
│       ├── project.yml       # Main project configuration
│       ├── manifests/        # Project related static yaml manifests
│       └── values/
│           └── argocd.yaml   # Every app can get it's own values file
├── README.md
├── renovate.json             # Preconfigured renovatebot for heqet config
├── resources/
│   ├── manifests/            # Your static manifests go here
│   │   └── foobar.yaml       
│   ├── networkpolicy.yml     # NetworkPolicies & create groups of policies
│   ├── repos.yml             # Helm Chart Repositories aliases
│   └── snippets/             # Value Snippets can be included into apps
│       └── tmpdirs.yaml      # They will be merged with all other app values 
└── values.yaml               # Defaults & main config for heqet
```
