Git Ops has four principles:

* The first principle is about the declarative vs imperative approach.
  git ops demands the entire system including infrastructure and applications manifest to be declared in a declarative state.

* Make use of git, all the declarative files, also known as the desired state is stored in a git repository, to apply any changes happens in the declarative file automatically.

* Git ops also known as software agents, automatically pull the desired state from the git repository and apply them in one or more environments or clusters.
  The git ops operator can run in one of the cluster and can make or push changes to other clusters as well.

* Reconciliation: The git ops operator also make sure that the entire system is self-healing to reduce the risk of human errors.
  The operator continuously loops through three steps, observe, diff(compare the previous step to the actual state in the cluster) and act