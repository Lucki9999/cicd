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
kubectl create ns flux #This will allow us hold all our info in a single ns

Install flux into the cluster
export GHUSER=Lucki9999
fluxctl install \
--git-user=${GHUSER} \
--git-email=${GHUSER}@users.noreply.github.com \
--git-url=git@github.com:${GHUSER}/cicd.git \
--git-path=flux/example-app/configmaps \
--git-branch=master \
--namespace=flux | kubectl apply -f -


flux bootstrap git \
  --url=https://github.com/Lucki9999/cicd.git \
  --username=Lucki9999 \
  --password=DevOps@9999 \
  --token-auth=true \
  --path=flux/example-app

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

flux bootstrap github \
  --owner=Lucki9999 \
  --repository=cicd \
  --path=flux/example-app \
  --branch=master \
  --personal
  
To setup a default ns for flux
export FLUX_FORWARD_NAMESPACE="flux"
To display logs
kubectl -n flux logs flux-74df595c5-6m69k


To authenticate flux to Git repo
Generate SSH keys
fluxctl identity
Add the key
Go to repo --> settings --> Deploy keys --> add the ssh keys given in previous step --> allow write access --> Add key
Here flux will talk to Git repo every 5 mins and sync the kubernetes cluster
#To sync the flux ssh keys manually
fluxctl sync

```
