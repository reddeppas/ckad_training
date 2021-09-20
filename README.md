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

