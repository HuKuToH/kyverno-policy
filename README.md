# Kyverno policy for replace default registry in pods managed k8s clusters

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
Change [line 21](https://github.com/HuKuToH/kyverno-policy/blob/9be5173cf5aefc3f6e1c830d5f8ef3ad5e6d358a/mirror-docker-hub.yaml#L21) and [line 40](https://github.com/HuKuToH/kyverno-policy/blob/9be5173cf5aefc3f6e1c830d5f8ef3ad5e6d358a/mirror-docker-hub.yaml#L40) replace docker.io to \<your-k8s-default-registry\> and mirror.gcr.io to \<your-mirror-registry\>
```
kubectl apply -f mirror-docker-hub.yaml
```
