# Certified Kubernetes Administrator 



### Architecture

##### kube-controller-manager:

##### kubelet:

##### kubeproxy

##### scheduler

##### kube-api server


##### Etcd:

  ETCDCTL version 2 supports the following commands:

        ```
          etcdctl backup
          etcdctl cluster-health
          etcdctl mk
          etcdctl mkdir
          etcdctl set

        ```

  Whereas the commands are different in version 3

        ```
          etcdctl snapshot save
          etcdctl endpoint health
          etcdctl get
          etcdctl put
        ```

  To set the right version of API set the environment variable ETCDCTL_API command
            ```
              export ETCDCTL_API=3

              kubectl exec etcd-master -n kube-system — sh -c “ETCDCTL_API=3 etcdctl get / –prefix –keys-only –limit=10 –cacert /etc/kubernetes/pki/etcd/ca.crt –cert /etc/kubernetes/pki/etcd/server.crt –key /etc/kubernetes/pki/etcd/server.key”

              ```
  
  ##### PODs

    ```
    kubectl run nginx --image nginx 
    ```

##### Replication Controller

Replication Controller api version is V1. and Selector is not required in the yaml defination file.

        ```
            kubectl create -f 
            apiVersion: v1
            kind: ReplicationController
            metadata:
              name:
              labels:
                app: webapp
                type: frontend
            spec:
             template:
               metadata:
                 name: webapp-pod
                 labels:
                   app: webapp
                   type: frontend
               spec:
                 containers:
                 - name: nginx-container
                   image: nginx
             replicas: 2         
         ```
    

##### Replica Set

 High Availability , Load Balancing and Scaling. apiversion apps/v1



##### Deployments


Create a NGINX Pod
```
  kubectl run nginx --image=nginx
```

Generate POD Manifest YAML file by providing -o yaml and Use –dry-run option for not creating the nginx pod

```
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

Create a deployment

```
kubectl create deployment --image=nginx nginx
```

Generate Deployment YAML file -o yaml and Don’t create it –dry-run

```
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
```

Generate Deployment YAML file using -o yaml option. Don’t create it use –dry-run option with 4 Replicas –replicas=4 and save it to a file.

```

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

```

Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

```
kubectl create -f nginx-deployment.yaml
```


In k8s version 1.19+, we can specify the –replicas option to create a deployment with 4 replicas.

```
kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
```

##### Namespace:

```
kubectl config set-context $(kubectl get current-context) --namespace=dev
```

##### Imperative  vs Declarative 

```
kubectl run nginx --image=nginx

kubectl create deployment nginx --image=nginx

kubectl expose deployment nginx --port=80

kubectl create deployment nginx

kubectl set image deployment nginx nginx=nginx:1.18

kubectl scale deployment nginx --replicas=5

kubectl create -f nginx.yaml

kubectl replace -f nginx.yaml

kubectl delete -f nginx.yaml
```

```
kubectl apply -f nginx.yaml
```

###### POD
Generate POD Manifest YAML file (-o yaml). Don’t create it

```
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

###### Service
Create a Service named nginx of type NodePort to expose pod nginx’s port 80 on port 30080 on the nodes:

```
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml

```

Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379

```
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```

(This will automatically use the pod’s labels as selectors)

OR

```
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 
```

This will not use the pods labels as selectors, instead it will assume selectors as app=redis. 
You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. 
So generate the file and modify the selectors before creating the service)
