You can delete all the pods in a single namespace with this command:

```
kubectl delete --all pods --namespace=common
```
You can also delete all deployments in namespace which will delete all pods attached with the deployments corresponding to the namespace

```
kubectl delete --all deployments --namespace=common
```
You can delete all namespaces and every object in every namespace (but not un-namespaced objects, like nodes and some events) with this command:

```
kubectl delete --all namespaces
```
However, the latter command is probably not something you want to do, since it will delete things in the kube-system namespace, which will make your cluster not usable.

This command will delete all the namespaces except kube-system, which might be useful:

```
for each in $(kubectl get ns -o jsonpath="{.items[*].metadata.name}" | grep -v kube-system);
do
  kubectl delete ns $each
done
```

update grafana with only values changed
```
helm upgrade --install grafana charts/grafana/ -f charts/grafana/values.yaml
kubectl rollout restart deployment grafana
```

