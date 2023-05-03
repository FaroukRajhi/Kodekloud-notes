# Find out the swapfile used on this system and save its exact path

swapon --show

# Format the 21MB partition as swap

sudo mkswap /dev/vdb2
sudo swapon /dev/vdb2

# Increase the existing swap (i.e /swapfile) size by 1GB.

sudo dd if=/dev/zero of=/swapfile bs=1M count=1024 oflag=append conv=notrunc


Disable the swap file:


sudo swapoff /swapfile



Setup the file as a swap file again.


sudo mkswap /swapfile



Enable again swaping:

sudo swapon /swapfile

# Resize the /dev/vdb3 partition  to 21MB.

sudo cfdisk /dev/vdb



