# kind-multinode-local

In K8s-multinode-local project we made a kubernetes kluster with one master and more nodes using VM as nodes.
The evolution VM -> docker has inspired the "kind" project: replace VM with docker containers already provisioned as nodes images.

### Create a one node cluster:
	kind create cluster			# cluster name: kind
	kind create cluster --name kind-new

### Create a multinode cluster:
	cat <<EOF | kind create cluster --config=-
	kind: Cluster
	apiVersion: kind.x-k8s.io/v1alpha4
	nodes:
	- role: control-plane
	- role: worker
	- role: worker

### Create a HA control-plane:
	cat <<EOF | kind create cluster --config=-
        kind: Cluster
        apiVersion: kind.x-k8s.io/v1alpha4
        nodes:
	- role: control-plane
	- role: control-plane
	- role: control-plane
	- role: worker
	- role: worker
	- role: worker

After cluster creation ans configuration, kubectl can beused.
The new cluster context will be inserted in ~/.kube/config.

### Delete cluster
	kind delete cluster [--name kind]

## The kind project on github:
- (https://kind.sigs.k8s.io/docs/user/ingress/)

