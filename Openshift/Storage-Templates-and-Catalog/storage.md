To persist data processed by the containers, we attach a persistent volumes to the containers when they are created.
The data processed by the container is now placed in this volume, thereby retaining it permanently.
Openshift leverages the k8s persistent volume framework to provision storage for a cluster.
Plugins:
- Local
- iSCSI
- Fiber channel
- NFS
- GlusterFS
- Ceph RDB
- Openstack Cinder
- AWS EBS
- GCE Persistent disk.
- Azure Disk.
- Azure File.
- VMWare vSphere

The storage added to the openshift cluster is available across the cluster as a single large pool of persistent volume resources.
From this, each project can claim the required amount of storage using persistent volume claims.

We can create storage from web console or CLI

Create a PVC the go to deployment configuration and click add storage