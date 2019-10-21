# Retrieving address for Free Kubernetes Cluster

View the namespace where IBPv2 network reside. In the example below, `b4ecd3` is the namespace we are going to target in the subsequent steps.

```console
$ kubectl get ns
b4ecd3           Active   4d1h
default          Active   4d2h
ibm-cert-store   Active   4d2h
ibm-observe      Active   20h
ibm-system       Active   4d2h
ibpinfra         Active   4d1h
kube-public      Active   4d2h
kube-system      Active   4d2h
```

Get the NodePort of the operation port for peer. In the example below, operation NodePort for `peer0org1` is `32003`:

```console
$ NS=b4ecd3
$ kubectl get service -n $NS
NAME        TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                                      AGE
orderer0    NodePort   172.21.254.167   <none>        7050:30520/TCP,8443:31422/TCP,8080:30420/TCP,7443:30693/TCP                  3d22h
ordererca   NodePort   172.21.25.240    <none>        7054:31733/TCP,9443:32569/TCP                                                3d22h
org1ca      NodePort   172.21.230.161   <none>        7054:32720/TCP,9443:31767/TCP                                                4d
peer0org1   NodePort   172.21.23.30     <none>        7051:31306/TCP,7052:32229/TCP,9443:32003/TCP,8080:31109/TCP,7443:30710/TCP   3d23h
peer0org5   NodePort   172.21.125.141   <none>        7051:30573/TCP,7052:31110/TCP,9443:32320/TCP,8080:30038/TCP,7443:31315/TCP   3d17h
```

Get the public IP of the Kubernetes cluster. In the example below, the **Public IP** is `184.172.247.204`

```console
CLUSTER=aldred
ibmcloud ks workers --cluster $CLUSTER
OK
ID                                                 Public IP         Private IP      Machine Type   State    Status   Zone    Version
kube-hou02-pabc5ec22b156647589c380a9c135e5eae-w1   184.172.247.204   10.76.196.182   free           normal   Ready    hou02   1.13.6_1522
```

Consolidate the `NodePort` and public IP together:

```console
PEER_ADDRESS=https://184.172.247.204:32003
```
