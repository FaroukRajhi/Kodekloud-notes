Your code get transformed into a build to a container image.
That build can be a container image.
As docker build process.
A build config, is the actual configuration that takes place of dockerfile "yaml manifest file", to take that source code and create a container image off it.
These build configs are automatically created for you via a build strategy.
A simple demo:

apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: sockshop
  namespace: faroukrajhi4-dev
spec:
  source:
    git:
      ref: master
      uri: 'https://github.com/mosuke5/microservices-demo.git'
    type: Git
  strategy:
    type: Source
    sourceStrategy:
      from:
      // from an existing image stream
      // It is a container inside a container image
        kind: ImageStreamTag
        name: 'ruby:2.7'
        namespace: openshift
      env: []
  triggers:
    - type: ImageChange
      imageChange: {}
    - type: ConfigChange

Build using CLI
oc start-build sockshop