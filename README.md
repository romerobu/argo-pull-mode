# argo-pull-mode


1. Install gitops operator in hub cluster and in all managed clusters

domain=sandbox3297.opentlc.com
cluster=dev-1 
password=tMxw8-bz4TS-Ww43g-5bYLm

oc login -u kubeadmin https://api.$cluster.$domain:6443 -p $password

oc apply -f bootstrap/

cluster=dev-2 
password=75Enh-ZjZEi-ihfGb-VCaG4

oc login -u kubeadmin https://api.$cluster.$domain:6443 -p $password

domain=sandbox3297.opentlc.com
cluster=play-1 
password=iA2hg-bcIAP-kWidT-Lf6i2

oc login -u kubeadmin https://api.$cluster.$domain:6443 -p $password

oc apply -f bootstrap-managed-clusters/05-cluster-role-sa.yaml

domain=sandbox3297.opentlc.com
cluster=play-2
password=x7HeH-4Gkjc-7KdAH-dN5zy

oc login -u kubeadmin https://api.$cluster.$domain:6443 -p $password

oc apply -f bootstrap-managed-clusters/05-cluster-role-sa.yaml

Add all managed cluster to a cluster set called as per environment: dev, play etc.

2. Then create GitOpsCluster in hub cluster and placement

oc apply -f 01-ManagedClusterSetBinding.yaml
oc apply -f 02-placement.yaml
oc apply -f 03-gitops-cluster.yaml