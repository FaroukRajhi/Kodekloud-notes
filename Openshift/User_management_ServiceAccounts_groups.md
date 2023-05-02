* Openshift user is a person that can log and authenticate into a system.

* System User: like the cluster admin, the root of the system itself.
Each user can have a granular permissions: may have read only, read and write in specific namespace, or everything.

We can create a user using CLI : oc create user <username>
Next you have to create an identity for that user: oc create identity allow_all: <username>.
Next we need to map that user so we can use: oc create iuserdentitymappong allow_all <username>.at user
We can delete that user : oc delete user <username>.

* Service account: have direct access the API.
We can really create a service account for a specific job.
oc create sa <name>
confirm account oc get sa
Add policy to the service account: oc policy add-role-to-user view (read only)system:serviceaccount:project name :sa name

* Group: are a collection of users
Create group and add role/ role binding