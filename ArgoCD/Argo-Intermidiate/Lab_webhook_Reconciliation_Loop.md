# To eliminate this reconciliation delay, create a git webhook configuration in Gitea


    Repository - gitops-argocd

    Target URL - <Argocd-url>/api/webhook

    POST Content Type – application/json

    Trigger On – Push Events

To create a webhook follow below steps:


a. Login to the Gitea UI.

b. Click on gitops-argocd repository.

c. Click on Settings

d. Click on Webhooks

e. Click on Add Webhook and select Gitea

f. Enter https://serive-ip:nodePort/api/webhook in Target URL

g. Set POST Content Type to application/json

h. Select Push Events under Trigger On

i. Finally click on Add Webhook

