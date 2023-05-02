# Install a Non-HA v2.4.11 ArgoCD within argocd namespace.

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.11/manifests/install.yaml

# Install argo Cli

curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.11/argocd-linux-amd64
chmod +x /usr/local/bin/argocd

