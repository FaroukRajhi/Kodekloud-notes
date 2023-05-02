If the rating service slows down for some reason, we will have requests queued at it which is going to cause requests on the review service to be queued up.

Timeout to fail

# update the virtualservice configuration to timeout after a period of 3 seconds for all calls to the httpbin service.

apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: httpbin
  namespace: default

spec:
  gateways:
  - httpbin-gateway
  hosts:
  - httpbin.example.com
  http:
  - fault:
      abort:
        httpStatus: 400
        percentage:
          value: 50
    timeout: 3s
    match:
    - uri:
        prefix: /status
    - uri:
        prefix: /delay
    - uri:
        prefix: /html
    route:
    - destination:
        host: httpbin
        port:
          number: 8000
