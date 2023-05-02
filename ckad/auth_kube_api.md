How kube-apiserver authenticate?
There are different authentication mechanisms that can be configured.

* List of username/password in a static password file (csv file) specified in kube-apiserver configuration
* Username and token in static token file.
* Authenticate using certificates.
* Another option (Identity services)is to connect to third party authentication protocols. like LDAP,Kerberos etc..
