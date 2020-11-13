# kind-bootstrap

Local Kubernetes bootstrap for coding challenges, using [kind](https://kind.sigs.k8s.io/).

It spins up a cluster with:
- 1 master and 2 workers with different containerd and kubelet versions ([1.17](./nodes/Dockerfile.17), [1.18](./nodes/Dockerfile.18))
- one of the worker nodes has a _"/sensitive"_ filesystem mount
- worker nodes also support the runsc runtime ([gVisor](https://gvisor.dev/))

## Setup

Install [Docker](https://docs.docker.com/get-docker/) + [kind](https://github.com/kubernetes-sigs/kind/releases) and run:

```bash
$ git clone https://github.com/MarshallWace/kind-bootstrap.git
$ cd kind-bootstrap/

$ kind create cluster --config cluster.yaml --name mw
Creating cluster "mw" ...
 ✓ Ensuring node image (ghcr.io/marshallwace/kind-node:17) 🖼
 ✓ Ensuring node image (ghcr.io/marshallwace/kind-node:18) 🖼
 ✓ Ensuring node image (kindest/node:v1.18.8) 🖼
 ✓ Preparing nodes 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-mw"

$ kubectl get nodes --context kind-mw
NAME               STATUS     ROLES    AGE   VERSION
mw-control-plane   Ready      master   75s   v1.18.8
mw-worker          Ready      <none>   41s   v1.17.5
mw-worker2         Ready      <none>   41s   v1.18.8
```

## Cleanup

```bash
$ kind delete cluster --name mw
```
