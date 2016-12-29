# Ceph Helm

### Quckstart

Assuming you have a Kubeadm managed Kubernetes 1.5 cluster and Helm 2.1 setup[1], you can get going straight away! [2]

From the root of this repo run:

```
helm serve &
helm repo add marina http://127.0.0.1:8879/charts

./build-all.sh

helm repo update

#Label the nodes that will take part in the Ceph cluster
kubectl get nodes -L kubeadm.alpha.kubernetes.io/role --no-headers | awk '$NF ~ /^<none>/ { print $1}' | while read NODE ; do
  kubectl label node $NODE --overwrite mariadb-server=enabled
done

#Deploy mariadb to the namespace setup above
helm install marina/mariadb --namespace mariadb --debug --dry-run

```
