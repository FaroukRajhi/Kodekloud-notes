It's a free and open source service mesh that provides an efficient way to secure, connect and monitor services.
Istio implements these proxies using an open-source high performance proxy known as "Envoy".
The proxy talk to a server side component known as the control plane.
Control plane consisted of three components named:
* Citadel: Manage certificate generation.
* Pilot: helped with service discovery.
* Galley: helped in validating configuration files.

The three components were later combined into a single daemon called "Istiod".
Each service or port has a separate component in it, along with Envoy proxy called "istio agent".
The istio agent is responsible for passing configuration secrets to the Envoy proxies.
