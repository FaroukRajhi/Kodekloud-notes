# The application outputs logs to the file /log/app.log. View the logs and try to identify the user having issues with Login.

kubectl -n elastic-stack exec -it app -- cat /log/app.log

# Edit the pod to add a sidecar container to send logs to Elastic Search. Mount the log volume to the sidecar container.

spec:
  containers:
  - name: app
    image: kodekloud/event-simulator
    volumeMounts:
    - mountPath: /log
      name: log-volume

  - name: sidecar
    image: kodekloud/filebeat-configured
    volumeMounts:
    - mountPath: /var/log/event-simulator/
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      // directory location on host
      path: /var/log/webapp
      // this field is optional
      type: DirectoryOrCreate
