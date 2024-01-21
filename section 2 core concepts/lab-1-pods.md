How many pods exist on the system?
```shell
kubectl get pods
```
Create a new pod with the nginx image.
```shell
kubectl run nginx --image=ngnix
```
**What is the image used to create the new pods?**
```shell
kubectl describe pod pod-name | grep image
```
**Which nodes are these pods placed on?**
```shell
kubectl describe pod pod-name
```

**How many containers are part of the pod webapp?**
```shell
kubectl get pods -> column READY 1/2 -> 2 containers
kubectl describe pod webapp -> 2 containers
```
**What images are used in the new webapp pod?**
```shell
kubectl describe pod webapp 
```

**Delete the webapp Pod.**
```shell
kubectl delete pod webapp
```
**Create a new pod with the name redis and the image redis123. Use a pod-definition YAML file.**
```shell
vi mypod.yaml
apiVersion: v1
kind: Pod
metadata:
    name: redis
    labels:
        app: redis
spec:
    containers:
    - name: myredis
      image: redis123
```
```shell
kubectl create -f mypod.yaml
```

**Now change the image on this pod to redis. Once done, the pod should be in a running state.**
```shell
kubectl set image pod/redis myredis=redis:alpine
```
or
```shell
vi mypod.yaml
apiVersion: v1
kind: Pod
metadata:
    name: redis
    labels:
        app: redis
spec:
    containers:
    - name: myredis
      image: redis
kubectl delete pod redis
kubectl create -f mypod.yaml
```

**Get pod definition in yaml file**

```shell
kubectl get pod <pod-name> -o yaml > pod-definition.yaml
```

**To modify the properties of the pod** 
```shell
kubectl edit pod <pod-name> command
```
**properties editable**
```shell
- spec.containers[*].image
- spec.initContainers[*].image
- spec.activeDeadlineSeconds
- spec.tolerations
- spec.terminationGracePeriodSeconds
```