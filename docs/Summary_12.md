# 12.3 Summary
* Kubernetes is implemented as a set of loosely coupled components, using etcd as the storage for all data
* Kubernetes’ capacity to continuously converge to the desired state is implemented through various components reacting to well-defined situations and updating the part of the state they are responsible for
* Kubernetes can be configured in various ways, so implementation details might vary, but the Kubernetes APIs will work broadly the same wherever you go
* By designing chaos experiments to expose various Kubernetes components to expected kinds of failure, you can find fragile points in your clusters nad make your cluster more reliable