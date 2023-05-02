When a service tries to communicate with another service, there should be a way to confirm they're really who they say they are.
This is done by hardening traffic using verification options like: Mutual TLS and JSON web token validation.
For example when a the service A tries to reach the service B, the service B needs to know that the request is actually coming from the service A.
So the communication between the service A and the service B should be validated.
Other method is the end user's access to services, for this istio support request authentication using JSON web token validation or OpenID connect providers, such as: ORYHydra, Keycloak, firebase or google.
Check PeerAuthentication manifest file in documentation.

#  Complete this template as per the details mentioned below and once done apply them.

apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: demo-peer-policy
  namespace: demo-app
spec:
  mtls:
    mode: STRICT