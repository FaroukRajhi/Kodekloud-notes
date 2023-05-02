argocd account list

Dex Okta Connector
ArgoCD embeds and bundles Dex Connect as part of its installation.
Dex is an identity service that powers authentication for other applications.
When a user logs in through Dex, the user identity is usually stored and authenticated by an external IDP.
Dex bis between applications and the identity provider.

# Create a new Argocd account as per details mentioned below.


    Account Name: alice

    Capabilities: apikey, login

kubectl -n argocd patch configmap argocd-cm --patch='{"data":{"accounts.alice": "apiKey,login"}}'

# Update the password of the newly created account alice


    Account name: alice

    New Password: 

argocd account update-password --account alice

*** Enter password of currently logged in user (admin): admin123
*** Enter new password for user alice: alice123
*** Confirm new password for user alice: alice123

# Which ArgoCD resource is used to store RBAC policies in ArgoCD

ConfigMap argocd-rbac-cm is used to store RBAC policies in ArgoCD.

# Create a new role with create application access as per details below and assign it to user alice


    Role Name: create-app

    Project: any

kubectl -n argocd patch configmap argocd-rbac-cm \
--patch='{"data":{"policy.csv":"p, role:create-app, applications, create, *, allow\ng, alice, role:create-app"}}'

Login with alice user and check using:
argocd account can-i delete applications '*' 
