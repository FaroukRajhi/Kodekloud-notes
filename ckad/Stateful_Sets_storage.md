
When you specify a PVC under pod definition all replicated pods created by that stateful set tries to use and share te same volume.
There are some cases where each pod has its own volume and each instance has its own database.
So each pod need a PVC bound to a PV.

So how to automatically create a PVC for each pod in a stateful set?
You can achieve that using using a "VolumeClaimTemplates".
Instead of creating a PVC manually, and then specifying it in the stateful set definition file, you move the entire PVC definition into a section in stateful set. named "VolumeClaimTemplates":

spec:
  volumes:
metadata:
  name: data-volume
spec:
 accessModes:
  - ReadWriteOnce
 storageClassName: google-storage # Storage class name
 resources:
   requests:
     storage: 500Mi

# Dynamic storage 

Storage class from cloud storage.
Defined in definition file:
Apiversion: storage.k8s.io/storage

provisioner: kubernetes.io/gce-pd