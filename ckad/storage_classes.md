# Static provisioning volumes

Create a cloud disk storage then allocate it to a persistent volume.

# Dynamic provisioning volumes

With storage classes you can define a provisioner such as Google storage that can automatically provision storage on google cloud and attach that to pods when a claim is made.

That's called dynamic provisioning volumes !
You do that by creating a storage class object with the API version set to "storage.k8s.io/v1".
Then after defining kind:

metadata:
  name: google-storage
provisioner: kubernetes.io/gcp-pd

The pv and pvc are automatically created when the storage class is created.

For the pvc we specify the storage class name in the ovc definition under spec section:
  storageClassName: google-storage
That's how the PVC knows which storage class to use.

we can also define a parameters to specify the disk tDisk)