# K3d Setup

## Refer: [k3d.io](https://k3d.io) a wrapper of K3s(Lightweight Kubernetes: [k3s.io](https://github.com/k3s-io/k3s)) in docker

## K3d commands

```bash
brew install k3d

k3d version
```

### Create a local (cluster-name) as dev-cluster with 1 master server and 2 worker agents along with k3d private local-registry with (registry-name) as dev-registry.localhost with expose (registry-port) as 12345

```bash
k3d cluster create dev-cluster --servers 1 --agents 2 --registry-create dev-registry.localhost:12345
```

#### Tag and push local images to k3d local registry: dev-registry

```bash
docker tag <image-name>:<image-tag> k3d-<registry-name>:<registry-port>/<image-name>:<image-tag>
```

example: `docker tag demo-app:v1 k3d-dev-registry.localhost:12345/demo-app:v1`

#### Add this to your local /etc/hosts for automatic resolution of `k3d-dev-registry.localhost`

```bash
127.0.0.1 k3d-<registry-name>
```

#### Add this line to your local `/etc/hosts`

example: `127.0.0.1   k3d-dev-registry.localhost`

Pushing images to this registry will make them accessible to Pods in k3d cluster

```bash
docker push k3d-<registry-name>:<registry-port>/<image-name>:<image-tag>
```

example: `docker push k3d-dev-registry.localhost:12345/demo-app:v1`

##

### List the local clusters

```bash
k3d cluster list

k3d cluster ls
```

### Stop the local development-cluster

```bash
k3d cluster stop dev-cluster
```

### Start a local development-cluster

```bash
k3d cluster start dev-cluster
```

### Delete a local development-cluster

```bash
k3d cluster delete dev-cluster
```

### K3d list nodes

```bash
k3d node list
```

### Using kubectl on k3d local-cluster

```bash
kubectl cluster-info

kubectl cluster-info dump | less
```

### Using kubectl commands

```bash
# Display the k3d cluster config
k config view
# Display list of contexts
k config get-contexts
# Display the current-context
k config current-context
# Set the default context to k3d <cluster-name>
k config use-context dev-cluster
```

```bash
# List all nodes in all namespaces
k get nodes -A
# List all services in all namespaces
k get services -A
k get svc -A
# List all deployments in all namespaces
k get deploy -A
# List all pods in all namespaces
k get pods -A
# List all configmaps in all namespaces
k get configmaps -A
# List all secrets in all namespaces
k get secrets -A
# List all the k8s resources
k get all -o wide
# List all the k8s resources in all namespaces
k get -A all -o wide
```

```bash
# Watch all pods
k get pods -w -o wide
# Watch all deployments
k get deploy -w -o wide
# Watch all services
k get svc -w -o wide
# Watch all configmaps
k get configmaps -w -o wide
```

```bash
# Create kubectl resources
k apply -f <yaml-file-path>
# Delete kubectl resources
k delete -f <yaml-file-path>
# Delete kubectl specific resources
k delete -f <deploymnet-service-file.yaml>
k delete -f <config-maps-file.yaml>
```
