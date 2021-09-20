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

