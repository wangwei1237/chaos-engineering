# 12.2 Summary of key components
We covered quite a few components in this chapter, so before I let you go, I’ve got a little parting gift for you - a handy reference of the key functions of these components. Take a look at table 12.1. If you’re new to all of this, don’t worry - it will soon start feeling like home.

Table 12.1 Summary of the key Kubernetes components

| Component | Key function |
| --- | --- |
| kube-apiserver | Provides APIs for interacting with the Kubernetes cluster. |
| etcd | The database used by Kubernetes to store all its data. |
| kube-controller-manager | Implements the infinite loop converging the current state toward the desired one. |
| kube-scheduler | Scheduled pods onto nodes, trying to find the best fit. |
| kube-proxy | Implements the networking for Kubernetes services. |
| container networking interface (CNI) | Implements the pod-to-pod networking in Kubernetes. For example Flannel, Calico. |
| kubelet | Starts and stops containers on hosts, using a container runtime. |
| container runtime | Actually runs the processes (containers, VMs) on a host. For example Docker, containerd, CRI-O, Kata, gVisor. |

And with that, it’s time to wrap up!