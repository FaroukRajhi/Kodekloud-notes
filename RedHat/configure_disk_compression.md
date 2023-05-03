# Virtual Data Optimizer (VDO)

VDO helps us save storage space through zero block filtering, deduplication and compression.

# Zero block filtering

In this step vdo looks at all of the blocks on storage device and filters out blocks that contains only zeros.
Those are blocks that have no data.

# Deduplication

In this step vdo checks to see if data has been written to disk already in another place.
Otherwise being duplication (data = 101, data =101, data =101).
Any block of data that is found to be a duplicate won't get written to disk instead metadata, which is data about data will be updated to point to the existing copy already on the disk.
e. g : data = 101, data = 101, data   = 101, data = 101 ====> three blocks of data will point to the same copy , act as metadata.

# Compression

In the last phase vdo will compress the data that gets written to the disk each block of data is compressed and packed together to save space on the disk.
And since many compressed blocks may fit into a single physical block.
This can speed up the process of reading the data from a disk in addition to saving space.

# installing and enabling VDO

yum install vdo
systemctl enable vdo

# Using VDO with storage devices

we will use vdb with 10 gigabytes.

vdo create --name=vdo_storage --device=/dev/vdb --vdoLogicalSize=10G

To view information about vdo stats

vdostats --human-readable

And we will see the differences

Format vdo

mkfs.xfs -K /dev/mapper/vdo_storage
-K = tell xfs , not to send discard requests when creating the file system

Make sure everything as been updated and all the device nodes have been created by issuing a command:
udevadm settle

Then mount the vdo 

Then mount int to /etc/fstab

# VDO on RHEL 9

VDO is integrated in lvm.
It like an lvm volume and add vdo option to it.

E.g

we have /dev/vdb with 5 gigabytes.

First create a physical volume

pvcreate /dev/vdb

create volume group using that physical volume.

Next create a lvm volume with vdo options

lvcreate --type vdo -n vdo_storage -L 100%FREE -V 10G vdo_volume/vdo_pool1.

-L 100%FREE  : Tell lvm to use all of the free extents available => use all the space in the volume.
-V 10G : Lets us set the vdo logical size in this case 10G.
vdo_volume/vdo_pool1: create a vdo pool called vdo_pool1

format it then mount it