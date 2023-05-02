# Create below mentioned service monitors for ArgoCD within argocd namespace.


   1. argocd-metrics

   2. argocd-server-metrics

   3. argocd-repo-server-metrics

   4. argocd-applicationset-controller-metrics

Set metadata.labels.release to kode-kloud-prometheus-stack

vi argocd-metrics.yaml

apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: argocd-metrics
  namespace: argocd
  labels:
    release: kode-kloud-prometheus-stack
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-metrics
  endpoints:
  - port: metrics

Create a yaml definition for argocd-server-metrics:

vi argocd-server-metrics.yaml

apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: argocd-server-metrics
  namespace: argocd
  labels:
    release: kode-kloud-prometheus-stack
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-server-metrics
  endpoints:
  - port: metrics

Create a yaml definition for argocd-repo-server-metrics:


vi argocd-repo-server-metrics.yaml

apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: argocd-repo-server-metrics
  namespace: argocd
  labels:
    release: kode-kloud-prometheus-stack
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-repo-server
  endpoints:
  - port: metrics

Create a yaml definition for argocd-applicationset-controller-metrics:


vi argocd-applicationset-controller-metrics.yaml

apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: argocd-applicationset-controller-metrics
  namespace: argocd
  labels:
    release: kode-kloud-prometheus-stack
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: argocd-applicationset-controller
  endpoints:
  - port: metrics

kubectl apply -f argocd-metrics.yaml
kubectl apply -f argocd-server-metrics.yaml
kubectl apply -f argocd-repo-server-metrics.yaml
kubectl apply -f argocd-applicationset-controller-metrics.yaml

# Click on the Grafana button to access the Grafana UI, then login to the same using below credentials:


   Username: admin

   Password: Fetch the password using below command

# Configure an AlertManager Rule for ArgoCD, which will raise an alert when an Argocd application status is changed to OutOfSync.


To do the same edit prometheusrules called kode-kloud-prometheus-stac-alertmanager.rules under monitoring namespace, the YAML snippet that needs to be added in it is as below:

kubectl -n monitoring edit prometheusrules kode-kloud-prometheus-stac-alertmanager.rules

- name: ArgoCD Rules
  rules:
    - alert: ArgoApplicationOutOfSync    
      expr: argocd_app_info{sync_status="OutOfSync"} == 1 
      for: 5m   
      labels:                                        
        severity: warning
      annotations:
         summary: "'{{ $labels.name }}' Application has  
                    synchronization issue"

