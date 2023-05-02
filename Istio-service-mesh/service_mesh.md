Into each microservice we replace them with a single proxy in the form of a sidecar container.
The proxies communicate with each other through what is known as a data plane, and they communicate to a server side component called "Control plane".
Control plane manages all the traffic into and out of your services via proxies.
So all the networking logic is abstracted from your business logic code.
This approach is known as a service mesh.

# What is the service mesh?

It is dedicated and configurable infrastructure layer that handles the communication between services without having to change the code in a microservice architecture.
With the service mesh, you can configure how services talk to each other. => Traffic management.
When services talk to each other, you'll have mutual TLS,so your workloads will be secure => Security.
Service discovery which covers three main topics: Discovery (we will need to know at which IP and port services are exposed, they can find each other), Health check and LoadBalancing.