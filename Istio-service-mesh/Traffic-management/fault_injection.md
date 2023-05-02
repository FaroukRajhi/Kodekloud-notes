It helps us to see if our policies run efficiently and are not too restrictive.
We can inject errors into our virtual services, and this could be two different types of errors, delays and aborts.

E.g we going to inject a delay type of default in the mesh for rating virtual service, describes by percentage.

# Next, let us update the fault injection to abort 50% of the requests with a return code of HTTP 400

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