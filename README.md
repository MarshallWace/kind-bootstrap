# kind-bootstrap

## Setup

Install [Docker](https://docs.docker.com/get-docker/) + [kind](https://github.com/kubernetes-sigs/kind/releases) and run:

```bash
kind create cluster --config cluster.yaml --name mw
```

## Cleanup

```bash
kind delete cluster --name mw
```
