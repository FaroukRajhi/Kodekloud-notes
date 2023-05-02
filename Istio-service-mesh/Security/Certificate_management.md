When a service is started, it needs to identify itself to the mesh control plane and retrieve a certificate in order to serve traffic.
Istio only has a built-in certificate authority.
The istio agent creates a private key and certificate signing request and then sends the certificate signing request with its credentials to istiod for signing.
The CA in istiod validates the credentials carried in the CSR.
Then Its sign the CSR to generate the certificate.
The istio agent sends the certificates received from and the private key to Envoy proxy.
Istio agent monitors the expiration of the workload certificate.
