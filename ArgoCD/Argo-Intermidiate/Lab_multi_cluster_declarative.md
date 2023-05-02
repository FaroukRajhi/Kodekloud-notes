# Add a new git repository in ArgoCD

argocd repo add <gitea-url>/bob/gitops-argocd.git

# Create an Argocd application as per details mentioned below and sync it:


    Application Name: helm-random-shapes

    Project Name: default

    Sync Policy: Manual

    Sync Options: Auto-create Namespace

    Repository URL: <Gitea URL>/bob/gitops-argocd.git

    Path: ./helm-chart

    Cluster URL: https://kubernetes.default.svc

    Namespace: default

# As per the current ArgoCD configuration, in how many clusters ArgoCD can deploy the application right now?

argocd cluster list

# Add a cluster called cluster2 to the list of Argocd clusters.

argocd cluster add cluster2

# Where does ArgoCD store the new cluster data?

ArgoCD store the new cluster data in Secrets.

# Create an Argocd application as per details mentioned below and sync it:


    Application Name: health-check-app

    Project Name: default

    Sync Policy: Manual

    Sync Options: Auto-create Namespace

    Repository URL: <Gitea URL>/bob/gitops-argocd.git

    Path: ./health-check

    Cluster URL: https://controlplane-cluster2:6443

    Namespace: health-check


