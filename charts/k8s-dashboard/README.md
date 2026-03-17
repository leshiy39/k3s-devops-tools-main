```
kubectl create serviceaccount kubernetes-dashboard -n kube-system
kubectl create clusterrolebinding kubernetes-dashboard-admin   --clusterrole=cluster-admin   --serviceaccount=kube-system:kubernetes-dashboard
# Если уже попытались раскатать до этого
kubectl rollout restart deployment k8s-dashboard -n kube-system
```