# Add /dev/vdd to this volume group so that we gain more usable storage space.

sudo vgextend volume1 /dev/vdd

# Remove /dev/vdd from the volume group volume1.

sudo vgreduce volume1 /dev/vdd

# Resize the Logical Volume called smalldata to 1 Gigabyte.
This logical volume resides on the volume group called volume1.

sudo lvresize --size 1G volume1/smalldata

# Setup /dev/vde as an encrypted disk. The mapped device should be called secretdisk.

sudo cryptsetup open --type plain /dev/vde secretdisk
sudo cryptsetup --verify-passphrase open --type plain /dev/vde secretdisk

# Create an XFS filesystem on this mapped device called secretdisk.

sudo mkfs.xfs /dev/mapper/secretdisk

# Close the unencrypted mapped device called secretdisk.

sudo cryptsetup close secretdisk

# Format the /dev/vde device to be used with LUKS encryption

sudo cryptsetup luksFormat /dev/vde

