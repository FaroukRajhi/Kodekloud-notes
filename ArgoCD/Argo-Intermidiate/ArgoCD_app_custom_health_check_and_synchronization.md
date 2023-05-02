Create an Argocd application as per details mentioned below:


    Application Name: health-check-app

    Project Name: default

    Sync Policy: Manual.

    Sync Options: Auto-create Namespace

    Repository URL: <Gitea URL>/bob/gitops-argocd.git

    Path: ./health-check

    Cluster URL: https://kubernetes.default.svc

    Namespace: health-check

# Access the app using HealthCheckApp button on the top bar.
There are 4 Geometric shapes visible in the UI and Square is of orange color.

# Write a custom health-check script in ArgoCD to change the application health status if the TRAINGLE_COLOR is white in the configmap. The status should be as below


    Health Status = DEGRADED

    Health Message = Use any color other than White


 data:
    resource.customizations.health.ConfigMap: |
      hs = {}
      hs.status = "Healthy"
       if obj.data.TRIANGLE_COLOR == "white" then
          hs.status = "Degraded"
          hs.message = "Use any color other than White "
       end
      return hs

Patch argocd-cm configmap with this yaml


kubectl patch configmap argocd-cm -n argocd --patch-file patch.yaml 

# In gitops-argocd repository update the value of TRAINGLE_COLOR to red within health-check/configmap.yml file (you can either make changes directly from Gitea or clone the repository and add/push your changes). Later sync the application from ArgoCD UI, enable PRUNE and FORCE options while syncing the application to make sure changes are in effect immediately.

Login to the Gitea server and edit gitops-argocd/health-check/configmap.yml file, change value for TRIANGLE_COLOR from white to red. Finally commit the changes.


Now, login to the ArgoCD UI and click on SYNC for health-check-app application, enable PRUNE and FORCE options and click on SYNCHRONIZE then Ok.

# Enable the automatic SYNC for health-check-app application.

argocd app set --sync-policy=auto health-check-app

# Now, enable self-heal for health-check-app application.

argocd app set health-check-app --sync-policy=auto --self-heal

Delete all services in health-check namespace using kubectl -n health-check delete svc --all command.

So now, does ArgoCD app heal the live state automatically by creating back the deleted service?

# Let's enable auto-prune for the health-check-app application now. Then delete gitops-argocd/health-check/service.yaml file.

argocd app set health-check-app  --sync-policy=auto --self-heal --auto-prune

Notice that how Argocd will automatically remove service(s) from live state (cluster) as well.

