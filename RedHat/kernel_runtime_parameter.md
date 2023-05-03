# Turn on kernel.modules_disabled kernel runtime parameter, so that loading new kernel modules will be disabled.

sudo sysctl -w kernel.modules_disabled=1

# Use the sysctl command to make sure this kernel runtime parameter is actively enabling its settings:

sudo sysctl -w net.ipv6.conf.lo.seg6_enabled=1

# Adjust the value of this kernel runtime parameter, vm.swappiness, to 10.

After you set this to 10, also make the change persistent so that it will be auto-set to this value on the next reboot.

sudo vi /etc/sysctl.conf



Add below given code in this file and save it:

vm.swappiness=10



Apply the changes:

sudo sysctl -p

# Change the SELinux context of /var/index.html file to httpd_sys_content_t

sudo chcon -t httpd_sys_content_t /var/index.html

