Create an Argocd application from the UI as per details mentioned below


    Application Name: solar-system-app-1

    Project Name: default

    Sync Policy: Manual

    Sync Options: Auto-create Namespace

    Repository URL: <Gitea URL>/bob/gitops-argocd.git

    Path: ./solar-system

    Cluster URL: https://kubernetes.default.svc

    Namespace: solar-system

# Sync the project

Sync the solar-system-app-1 app from ArgoCD UI.


Access the Gitea server with below credentials

    username: bob

    password: bob@123


Access the ArgoCD UI and CLI with below credentials.

    User: admin

    Password: admin123

 For solar-system-app-1 app click on SYNC.

c. Keep all options as it is and click on SYNCHRONIZE

# Create an Argocd Application using CLI
argocd app create solar-system-app-2 \
--repo https://3000-port-dd26ac4917424360.labs.kodekloud.com/bob/gitops-argocd.gitt \
--path ./solar-system \
--dest-namespace solar-system \
--dest-server https://kubernetes.default.svc

# Synchronize the solar-system-app-2 application using Argocd CL

argocd app sync solar-system-app-2


