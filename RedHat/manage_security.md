# Edit the system-wide configuration of the SSH client and turn on X11 forwarding.

sudo vi /etc/ssh/ssh_config

Uncomment below given line or add it if doesn't exist:


ForwardX11 yes

# Edit the config file of the Squid proxy daemon. Modify it to deny access to the IP addresses defined in the ACL called localnet.

sudo vi /etc/squid/squid.conf

And change http_access allow localnet line to http_access deny localnet

# Edit the configuration of the Squid proxy daemon. Add a src type acl and name it vpn. The IP you should use in this acl is 203.0.110.5. Now add a new rule that tells the proxy server to allow access to the acl named vpn.

Edit /etc/squid/squid.conf file:

sudo vi /etc/squid/squid.conf



and save below given changes in it:


Add this line

acl vpn src 203.0.110.5



Add below given line in the same file before http_access deny all line:

http_access allow vpn

# Edit the configuration of the SSH server and configure it to use only IPv4 IP address family.

sudo vi /etc/ssh/sshd_config



Uncomment the below given line in it:

#AddressFamily any



and change it to (add it if doesn't exist):

AddressFamily inet

