# CKAD



### Architecture



##### Etcd:

  ETCDCTL version 2 supports the following commands:

  etcdctl backup
  etcdctl cluster-health
  etcdctl mk
  etcdctl mkdir
  etcdctl set

  Whereas the commands are different in version 3

  etcdctl snapshot save
  etcdctl endpoint health
  etcdctl get
  etcdctl put

  To set the right version of API set the environment variable ETCDCTL_API command

  export ETCDCTL_API=3
  
  kubectl exec etcd-master -n kube-system — sh -c “ETCDCTL_API=3 etcdctl get / –prefix –keys-only –limit=10 –cacert /etc/kubernetes/pki/etcd/ca.crt –cert /etc/kubernetes/pki/etcd/server.crt –key /etc/kubernetes/pki/etcd/server.key”
