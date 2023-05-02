# Deploy Bitnami sealed secret controller by creating an Argocd application using either UI or CLI and synchronize the app


   Application Name: sealed-secrets

   Project Name: default

   Sync Policy: auto

   Repository URL: https://bitnami-labs.github.io/sealed-secrets

   Repository Type: Helm

   Chart: sealed-secrets

   Version: 2.2.0

   Cluster URL: https://kubernetes.default.svc

   Namespace: kube-system

# Install kubeseal CLI version 0.18.0. Click on the KubeSeal button to take help from the documentation.

wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.18.0/kubeseal-0.18.0-linux-amd64.tar.gz
tar -xvzf kubeseal-0.18.0-linux-amd64.tar.gz kubeseal
sudo install -m 755 kubeseal /usr/local/bin/kubeseal

# Extract the sealed-secrets controller TLS certificate from kube-system namespace and store it in a file named /root/sealedSecret-publicCert.crt

kubectl -n kube-system get secret
kubectl -n kube-system get secret sealed-secrets-keyf5txr -o json | jq -r .data'."tls.crt"' | base64 -d > /root/sealedSecret-publicCert.crt

# Create /root/mysql-password_k8s-secret.yaml specification file for a generic Kubernetes secret called app-crds. Add below given secret data in it:


   username: admin-dev-group

   password: paSsw0rD-1erT-diS

   apikey: zaCELgL-0imfnc8mVLWwsAawjYr4Rx-Af50DDqtlx

kubectl create secret generic app-crds --from-literal=apikey=zaCELgL-0imfnc8mVLWwsAawjYr4Rx-Af50DDqtlx --from-literal=username=admin-dev-group --from-literal=password=paSsw0rD-1erT-diS -o yaml --dry-run=client > mysql-password_k8s-secret.yaml

# Use kubeseal CLI to create a sealed secret from the previously created definition file i.e mysql-password_k8s-secret.yaml. The sealed secrets should be stored in mysql-password_sealed-secret.yaml file. Further find below more details:


   Scope: cluster-wide

   Format: yaml

   Certificate: /root/sealedSecret-publicCert.crt

kubeseal -o yaml --scope cluster-wide --cert sealedSecret-publicCert.crt < mysql-password_k8s-secret.yaml > mysql-password_sealed-secret.yaml

# Replace the contents of gitops-argocd/sealed-secret/secret.yaml definition file in gitops-argocd repository with the contents of mysql-password_sealed-secret.yaml file (you just created in the previous question). You can either directly update this file on Gitea or clone and add/push your changes from command line.

cat mysql-password_sealed-secret.yaml

# Install argocd-vault-plugin version 1.12.0. Click on ArgocdVaultPlugin button to take help from the documentation.

curl -Lo argocd-vault-plugin https://github.com/argoproj-labs/argocd-vault-plugin/releases/download/v1.12.0/argocd-vault-plugin_1.12.0_linux_amd64
chmod +x argocd-vault-plugin 
mv argocd-vault-plugin /usr/local/bin

# There is a kubernetes secret definition file /root/secret.yaml, it has some placeholders for apikey:, username: and password:. We already have some secrets added in the Vault server which contain the original values for these placeholders.


Use argocd-vault-plugin and generate a secret manifest/definition file called /root/secret_updated.yaml with all the placeholders replaced with the actual values from the Vault server. Find below some useful details:


   Vault Env File: /root/vault.env

   Placeholder Secret Definition File: /root/secret.yaml

   Final Secret Definition File: /root/secret_updated.yaml

argocd-vault-plugin generate -c /root/vault.env - < /root/secret.yaml > /root/secret_updated.yaml

# Edit the argocd-repo-server deployment to add an init container to make argocd-vault-plugin utility available within this pod. To do this you need to follow few steps as below:


Add an Initcontainer as below:

      - name: download-tools
        image: alpine:3.8
        command: [sh, -c]
        env:
          - name: AVP_VERSION
            value: "1.7.0"
        args:
          - >-
            wget -O argocd-vault-plugin
            https://github.com/argoproj-labs/argocd-vault-plugin/releases/download/v${AVP_VERSION}/argocd-vault-plugin_${AVP_VERSION}_linux_amd64 &&
            chmod +x argocd-vault-plugin &&
            mv argocd-vault-plugin /custom-tools/
        volumeMounts:
          - mountPath: /custom-tools
            name: custom-tools



Add a Volume:

- name: custom-tools
   emptyDir: {}