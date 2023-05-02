An image stream essentially gives you the ability to update deployments on the fly with tags.
Let's say you make an update to a container image, and maybe that one update is a tag that goes from the latest version to version 3.4 for example.
In OpenShift, an Image Stream is an object that represents a logical pointer to a specific image, which can be used to deploy applications. Image Streams allow for automatic updates of images in your environment. When you create an Image Stream, you can specify the registry and repository where the image resides, as well as the tag or version of the image.

Image Streams also provide a way to manage and control access to images in a multi-tenant environment. By creating separate Image Streams for different teams or applications, you can restrict access to specific images and ensure that only authorized users can deploy them.

One of the key benefits of using Image Streams in OpenShift is that they allow for seamless image updates. When you update the image in the registry, OpenShift will automatically detect the new version and update the Image Stream accordingly. This ensures that all deployments using that Image Stream are automatically updated to the latest version of the image.

In summary, Image Streams in OpenShift provide a flexible and powerful way to manage and deploy images in a containerized environment, while also providing versioning and access control capabilities.

At that point, the image stream will look at wherever your container image is, whatever container  registry it's in, and then it can automatically make that change to your deployment.
Sp image stream do:
1. it creates and updates the container images in an ongoing way, so again, you have that level of abstraction where you don't have to go into manifest.
2. you can use a tag for the new version.
3. Rolling updates.
4. You can configure your builds and your deployments to look at an image stream and essentially get notifications for if a new image is added, for example, that can be deployed.
=> You can set this up in an automated and repeatable fashion.
5. The image stream doesn't contain actual image data, it goes and it looks at a container registry wherever the container registry exists and pulls the data from there.

The source images can be stored in a few different places: openshift container platform integrated registry, an external registry like docker hub etc..., 

To create an image stream, here is an example :

apiVersion: image.openshift.io/v1
kind: ImageStream
metadata:
  name: carts
  namespace: faroukrajhi4-dev
spec:
  lookupPolicy:
    local: false
  tags:
  - name: "0.4.8"
    from:
      kind: DockerImage
      name: weaveworksdemos/carts:0.4.8
    referencePolicy:
      type: source

Using CLI
oc new-app --image-stream=<namespace>/<image stream name>:0.4.8