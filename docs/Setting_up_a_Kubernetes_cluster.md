# 10.3 Setting up a Kubernetes cluster
Before we can continue with our scenario, you’re going to need access to a working Kubernetes cluster. The beauty of Kubernetes, is that you can get the cluster from various providers, and it should behave exactly the same! All the examples in this chapter will work on any conformant clusters and I will mention where there might be potential caveats. Therefore you’re free to pick whatever installation of Kubernetes is the most convenient for you.

For those who don’t have a Kubernetes cluster handy, the easiest way to get started is to deploy a single-node, local mini-cluster on your local machine with Minikube (https://github.com/kubernetes/minikube). Minikube is an official part of Kubernetes itself, and allows you to deploy a single node with single instances of all the Kubernetes control plane components inside of a virtual machine. It also takes care of the little-yet-crucial things like helping you easily access things running inside of the cluster.

Before continuing, please follow Appendix A to install Minikube. In this chapter, I’ll assume you’re following along with a Minikube installation on your laptop. I’ll also mention whatever might be different if you’re not. Everything in this chapter was tested on Minikube 1.12.3, and Kubernetes 1.18.3.

## 10.3.1 Starting a cluster
Depending on the platform, Minikube supports multiple virtualization options to run the actual VM with Kubernetes. The options differ for each platform and include:

* Linux: KVM or VirtualBox (running processes directly on the host is also supported)
* macOS: HyperKit, VMware Fusion, Parallels or VirtualBox
* Windows: Hyper-V or VirtualBox

For our purposes, you can pick any of the supported options and it should work all the same. But because I already made you install VirtualBox for the previous chapters and it’s a common denominator of all three supported platforms, I’d recommend we stick with VirtualBox.

To start a cluster, all you need is the `minikube start` command. To specify the VirtualBox driver, use the `--driver` flag. Run the following command from a terminal to start a new cluster using VirtualBox:

```shell
minikube start --driver=virtualbox
```

The command might take a minute, because minikube needs to download the VM image for your cluster and then start a VM with that image. When it’s done, you will see the output similar to the following. Someone took the time to pick relevant emoticons for each log message, so I took the time to respect that and copy verbatim. You can see that it used the VirtualBox driver like I requested and defaulted to give the VM 2 CPUs, 4GB of RAM and 2GB of storage. It’s also running Kubernetes v1.18.3 on Docker 19.03.12 (all in bold font).

```shell
😄  minikube v1.12.3 on Darwin 10.14.6 
✨  Using the virtualbox driver based on user configuration 
👍  Starting control plane node minikube in cluster minikube 
🔥  Creating virtualbox VM (CPUs=2, Memory=4000MB, Disk=20000MB) … 
🐳  Preparing Kubernetes v1.18.3 on Docker 19.03.12 … 
🔎  Verifying Kubernetes components… 
🌟  Enabled addons: default-storageclass, storage-provisioner 
🏄  Done! kubectl is now configured to use "minikube"
```

To confirm that it started OK, try to list all pods running on the cluster. Run the following command in a terminal:

```shell
kubectl get pods -A
```

You will see the output just like the following, listing the different components that together make the Kubernetes control plane. We will cover in detail how they work later in this chapter. For now, this command working at all proves that the control plane works.

```shell
NAMESPACE     NAME                  READY   STATUS    RESTARTS   AGE 
kube-system   coredns-66bff467f8-62g9p           1/1     Running   0          5m44s 
kube-system   etcd-minikube         1/1     Running   0          5m49s 
kube-system   kube-apiserver-minikube            1/1     Running   0          5m49s 
kube-system   kube-controller-manager-minikube   1/1     Running   0          5m49s 
kube-system   kube-proxy-bwzcf      1/1     Running   0          5m44s 
kube-system   kube-scheduler-minikube            1/1     Running   0          5m49s 
kube-system   storage-provisioner                1/1     Running   0          5m49s
```

We’re now ready to go. When you’re done for the day and want to stop the cluster, use `minikube stop`, and to resume the cluster use `minikube start`.

{% hint style='info' %}
**NOTE GETTING KUBECTL HELP**

You can use the command kubectl --help to get help on all available commands in kubectl. If you’d like more details on a particular command, use --help on that command. For example, to get help about the available options of the get command, just run kubectl get --help.
{% endhint %}

Time to get our hands dirty with the High Profile Project.