#Install flux
```sh
brew install fluxcd/tap/flux
```

#verify flux pre-requisities
```sh
flux check --pre
```

#Getting started
```sh
create ns 
kubectl create ns flux-system #This will allow us hold all our info in a single ns

Install flux into the cluster


export GITHUB_TOKEN=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
Note: To generate token Github --> users --> settings --> Developers settings --> personal access token   

flux bootstrap github \
  --owner=Lucki9999 \
  --repository=cicd \
  --path=flux/environments/staging \
  --branch=master \
  --token-auth \
  --personal
  
To setup a default ns for flux
export FLUX_FORWARD_NAMESPACE="flux"
To display logs
kubectl -n flux logs flux-74df595c5-6m69k

#To reconcile away from flux interval
flux reconcile kustomization flux-system --with-source

To authenticate flux to Git repo
Generate SSH keys
fluxctl identity
Add the key
Go to repo --> settings --> Deploy keys --> add the ssh keys given in previous step --> allow write access --> Add key
Here flux will talk to Git repo every 5 mins and sync the kubernetes cluster
#To sync the flux ssh keys manually
fluxctl sync



```
