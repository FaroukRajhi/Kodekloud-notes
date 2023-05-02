Istio provides a flexible approach to access control for inbound traffic.
We can control which service can reach which service.
For example we would like to only allow the service A to access service B, and not other services.
Authorization actions:
Custom: Allows an extension to handle the request.
Deny: Denies a request from going through.
Allow: Allows a request to go through.

Check AuthorizationPolicy manifest file documentation.

#  node. Complete this template as per the details mentioned below and once done apply them.

a. The policy must be named as demo-api-policy

b. Design the policy to allow all GET requests from demo-app namespace to demo-api namespace.

apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: demo-api-policy
  namespace: demo-api
spec:
  action: ALLOW
  rules:
  - from:
    - source:
        namespaces: ["demo-app"]
    to:
    - operation:
        methods: ["GET"]