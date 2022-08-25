# Sample Kubectl plugins

## KUBECTL plugin to dump all container logs from a given namespace

If you need to look at ALL the container logs from a namespace, currently, there isn’t an option (that I am aware of) to do so with kubectl today. This simple kubectl plugin solves the issue by dumping the logs from all the pods/containers in a given namespace. Useful for troubleshooting apps and cluster issues that may have multiple labels or deployment files (no common attributes, like pods within kube-system) but all reside in the same namespace.

## Deployment/Install

Copy the script in your OS path and set the execute permissions. 

To run this plugin execute - 
```
kubectl nslogs -n namespace [ SINCE - only return logs newer than a relative duration like 5s, 2m, or 3h. Without any values, defaults to all logs ]
```
E.g.
```
kubectl nslogs -n kube-system 5s
```

CTRL+C to STOP/terminate. 

Verified to work on MacOS and Linux. 

---
## KUBECTL plugin to dump ownerReferenceObjects 

This simple kubectl plugin does a recursive walkthru of a given Kubernetes resource and lists out all the ownerReferenceObjects chain. 

## Deployment/Install

Copy the script in your OS path and set the execute permissions. 

To run this against a non-namespaced resource execute - 
```
kubectl getownerref object object-name
```

To run this against a non-namespaced resource execute - 
```
kubectl getownerref -n namespace object object-name
```
A sample output is provided here - 

```
kubectl getownerref VSphereMachine -n demo1 workload-vsphere-tkg3-control-plane-69vrb-vrpj8

VSphereMachine/workload-vsphere-tkg3-control-plane-69vrb-vrpj8 == Is Owned by == KubeadmControlPlane/workload-vsphere-tkg3-9r645
KubeadmControlPlane/workload-vsphere-tkg3-9r645                == Is Owned by == Cluster/workload-vsphere-tkg3

VSphereMachine/workload-vsphere-tkg3-control-plane-69vrb-vrpj8 == Is Owned by == Machine/workload-vsphere-tkg3-9r645-gqwx6
Machine/workload-vsphere-tkg3-9r645-gqwx6                      == Is Owned by == KubeadmControlPlane/workload-vsphere-tkg3-9r645
KubeadmControlPlane/workload-vsphere-tkg3-9r645                == Is Owned by == Cluster/workload-vsphere-tkg3
```
