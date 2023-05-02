There are four strategies to how you can create the build configuration:
1. Source to image (S2I): Is a tool to create docker-formatted container images.
   It produces  ready-to-run images,and it injects the application source into the container image and it assembles a new image.

2. Pipeline: Is a strategy to define a Jenkins pipeline, so you can execute it via the jenkins plugin.

3. Docker: is Literally just the docker build command.
   Openshift uses "Buildah" to create the the containers from scratch.

   Inside the buildConfig manifest :
   Strategy:
     type: Docker
     dockerfilePath: path


4. Custom: Helps developers define a custom builder images, For example you can build RPMs, you can build base images.
Check out the documentation.

Build Input: Source code GIT, Dockerfile, Binary, Image, Input secret (For db), External artifacts
