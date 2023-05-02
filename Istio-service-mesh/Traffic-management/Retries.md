When a service tries to reach another service, and for some reason, it fails, we can configure the virtual service to attempt that operation again.
This way you don't have to handle the retries within the application code.
You can retry configure settings, which basically says the number of times to try and the interval between them.
Istio by default has retries behavior which is 25 milliseconds.
configuration in virtual service manifest files:

retries:
  attempts: 3
  perTryTimeout: 2s

