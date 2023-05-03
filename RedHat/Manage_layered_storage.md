Manage layered storage using stratis.

# What is stratis

Is a local storage management tool for Linux.
It manages pools of physical storage and helps simplify storage management allowing complex storage configurations and to be deployed easily.
the central component of stratis is the storage pool.
And the storage pools are create from one or more disks or partitions.
Those are block devices.
And once the pools have been created, volumes can be created on top of the pools.

Through pools stratis enable some useful features such as (filesystem snapshots, Thin provisioning, Tiering).
Stratis is similar to lvm but is designed to be easier to configure deploy and manage.
Stratis uses the xfs filesystem

# Installing and starting Stratis

Yum install stratisd stratis-cli

Then enable its daemon

Create a stratis pool

stratis pool create my-pool /dev/vdc

For more disks

stratis pool create my-pool /dev/vdc /dev/vdd

List the pool

stratis pool list

# Creating a stratis filesystem

stratis fs create my-pool myfs1.
myfs1 being created on top of the pool.

See information

stratis fs

Mount it

# Adding storage devices to the stratis pool

stratis pool add-data my-pool /dev/vdb

Check the pool

stratis pool

# Filesystem snapshot with stratis

Allows us to use it as a backup later.

stratis fs snapshot my-pool myfs1-snapshot

Check startis fs

unmount the stratis filesystem


