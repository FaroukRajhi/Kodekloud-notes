The way you point within the cluster to another application through a service:
e.g replicas of stateful applications: one master (mysql) and two slaves.
We want to point the web server to the master database server only:

A headless service is created like a normal service, but does not have an IP if its own.

Create a headless service:

Like a service but in definition set ClusterIP: None
Then in pod definition for mysql:
Under container add:
  subdomain : service-name
  hostname: mysql-pod

finally specify the service name in stateful definition under spec section:

serviceName : <service-name>
