# What is the user used to execute the sleep process within the ubuntu-sleeper pod?

kubectl exec ubuntu-sleeper -- whoami

# pod ubuntu-sleeper to run the sleep process with user ID 1010.

spec:
  securityContext:
    runAsUser: 1010
  containers:
  - command:
    - sleep
    - "4800"

# Update pod ubuntu-sleeper to run as Root user and with the SYS_TIME capability.

image: ubuntu
    name: ubuntu-sleeper
    securityContext:
      capabilities:
        add: ["SYS_TIME"]

# Now update the pod to also make use of the NET_ADMIN capability.

    image: ubuntu
    name: ubuntu-sleeper
    securityContext:
      capabilities:
        add: ["SYS_TIME", "NET_ADMIN"]
