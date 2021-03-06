
# concourse-k8-pipeline
## Preparing

1. Create `stage` and `prod` namespaces
1. Create `concourse` serviceaccount in both namespaces
1. Create `concourse` rolebinding which is bound `edit` clusterrole in both namespaces

```
for ns in stage prod; do
  kubectl create ns $ns
  kubectl create sa concourse -n $ns
  kubectl create rolebinding concourse --clusterrole edit --serviceaccount ${ns}:concourse -n $ns
done
```

1. Clone https://github.com/zlabjp/kubernetes-scripts
1. Copy a kubeconfig of `concourse` serviceaccount of each namespace using `create-kubeconfig` in kubernetes-scripts repository
1. Paste a kubeconfig to `stage-kubeconfig` and `prod-kubeconfig` in `ci/vars.yml`

```
$ git clone https://github.com/zlabjp/kubernetes-scripts.git && cd kubernetes-scripts
$ ./create-kubeconfig concourse --namespace stage
$ ./create-kubeconfig concourse --namespace prod
```

## License

All files in this repository are released under the MIT License, see LICENSE.txt.
# concourse-k8-pipeline
