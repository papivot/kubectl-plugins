# KUBECTL plugin to dump ownerReferenceObjects 

This simple kubectl plugin does a recursive walkthru of a given Kubernetes resource and lists out all the ownerReferenceObjects chain. A sample output is provided here - 

```
kubectl getownerref VSphereMachine -n demo1 workload-vsphere-tkg3-control-plane-69vrb-vrpj8

VSphereMachine/workload-vsphere-tkg3-control-plane-69vrb-vrpj8 == Is Owned by == KubeadmControlPlane/workload-vsphere-tkg3-9r645
KubeadmControlPlane/workload-vsphere-tkg3-9r645                == Is Owned by == Cluster/workload-vsphere-tkg3

VSphereMachine/workload-vsphere-tkg3-control-plane-69vrb-vrpj8 == Is Owned by == Machine/workload-vsphere-tkg3-9r645-gqwx6
Machine/workload-vsphere-tkg3-9r645-gqwx6                      == Is Owned by == KubeadmControlPlane/workload-vsphere-tkg3-9r645
KubeadmControlPlane/workload-vsphere-tkg3-9r645                == Is Owned by == Cluster/workload-vsphere-tkg3
```
---
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
