# hostPath

 volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      // directory location on host
      path: /var/log/webapp
      // this field is optional
      type: Directory
    
# Create a Persistent Volume with the given specification

* Volume Name: pv-log
* Storage: 100Mi
* Access Modes: ReadWriteMany
* Host Path: /pv/log
* Reclaim Policy: Retain

spec:
  persistentVolumeReclaimPolicy: Retain
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/log

# Let us claim some of that storage for our application. Create a Persistent Volume Claim with the given specification.



* Volume Name: claim-log-1
* Storage Request: 50Mi
* Access Modes: ReadWriteOnce

spec:
  accessModes:
    - ReadWriteMany // mode : bound
  resources:
    requests:
      storage: 50Mi

