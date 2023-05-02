When you log into the openshift web console, the interface with the various deployment options you see the catalog.
Catalogs are databases, runtime, cache.
We can create a custom catalog.
To create a new template, create a YAML file and specify the app version as v1 and kind as template.
It is a bundle of db, config map , secret etc.. separated by (---)
check out the documentation.