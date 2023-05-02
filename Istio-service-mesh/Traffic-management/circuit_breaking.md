We know that the product service communicate with other services.
If for some reason a service breaks or slows down and it is unable to serve the product service, all requests from the product service will pile up the other services.
Essentially creating a delay as the product services is waiting for responses from the other service.
The circuit breaking allows us to create resilient microservice applications that will limit the impact of the failures or other network-related issues.
We can limit the number of requests coming.
configuration in destination rule:

trafficPolicy:
  connectionPool:
    tcp:
      maxConnections: 3