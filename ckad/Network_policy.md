# Create a network policy to allow traffic from the Internal application only to the payroll-service and db-service

* Policy Name: internal-policy
* Policy Type: Egress
* Egress Allow: payroll
* Payroll Port: 8080
* Egress Allow: mysql
* MySQL Port: 3306

spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP