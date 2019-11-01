# Summary
If you try to bootstrap argocd using a kustomize deploy that uses namePrefix, the argocd-server pod terminates with the fatal error:
`time="2019-11-01T14:06:41Z" level=fatal msg="configmap \"argocd-cm\" not found"`

If you remove the namePrefix, then it installs fine.

# Steps to reproduce

1. Spin up an empty k8s cluster -or- create a new namespace and edit the files in this repo to refer to that namespace
1. `kubectl apply -k dev/local/argocd`
1. `kubectl logs -l app.kubernetes.io/name=argocd-server`
1. `kubectl delete -k dev/local/argocd`
1. Edit the kustomization.yaml files to comment out the namePrefix setting
1. `kubectl apply -k dev/local/argocd`
1. `kubectl logs -l app.kubernetes.io/name=argocd-server`
