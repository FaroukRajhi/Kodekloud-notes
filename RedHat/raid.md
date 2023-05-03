# Add another device, /dev/vde, to the previously created array, /dev/md0.

sudo mdadm --manage /dev/md0 --add /dev/vde

# In your home directory you will find a directory called collection. Use the setfacl command recursively, so that ACL entries are modified on the directory itself but also all the files and subdirectories it may contain. The ACL permissions should allow the user called john to read, write and execute all entries within this directory.

setfacl --recursive --modify user:john:rwx collection/

# Edit disk quotas for the user called john. Set a soft limit of 100 megabytes and hard limit of 500 megabytes on /mnt partition.


sudo xfs_quota -x -c 'limit bsoft=100m bhard=500m john' /mnt/

