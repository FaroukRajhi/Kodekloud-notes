The three build triggers on openshift:

1. Webhook: Send Request to API when a change occurs.
   We have multiple webhooks: Github, Gitlab, Bitbucket, General.

2. The image change: The image stream tag change create an automatic build.
   When the image tag changes the image stream gets updated and ensures the latest.

3. Configuration changes: Pod Template change, Creates new replication controller.

We can specify the triggers type into yaml manifest of buildConfig:
triggers:
  - type: ImageChange
    imageChange: {}
  - type: ChangeConfig
     