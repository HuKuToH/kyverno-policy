# Kyverno policy for replace default registry in pods k8s

The rule replaces the default registries in your modules with the required mirror.
Saving you from having to manually fix your manifests/helm charts/kustomize.

## For example

```
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  securityContext:
    runAsUser: 0
  containers:
  - name: task-pv-container
    image: busybox:latest
```
```
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  securityContext:
    runAsUser: 0
  containers:
  - name: task-pv-container
    image: <your-registri-mirror.com>/busybox:latest
```


# Instal kuverno opertar
## Using helm
```
kubectl create ns kyverno
helm repo add https://kyverno.github.io/kyverno/
helm install kyverno kyverno/kyverno -n kyverno
```

# Apply policy
Change
```
kubectl apply -f mirror-docker-hub.yaml
```
