# Route using nmcli

nmcli connection modify eth1 +ipv4.route <network-ip> <interface-ip/cidr>

To delete route
nmcli connection modify eth1 -ipv4.route <network-ip> <interface-ip/cidr>

# Allow all traffic that is coming from any IP in this network range: 10.11.12.0 to 10.11.12.255 (i.e 10.11.12.0/24), add the required rule in the trusted zone and the rule must be permanent.

sudo firewall-cmd --add-source=10.11.12.0/24 --zone=trusted --permanent
