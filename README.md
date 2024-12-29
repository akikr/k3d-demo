# K3d Setup

## Refer: [k3d.io](https://k3d.io) a wrapper of K3s(Lightweight Kubernetes: [k3s.io](https://github.com/k3s-io/k3s)) in docker

## K3d commands

```bash
brew install k3d

k3d version
```

### Create a local (cluster-name) as `dev-cluster` with 1 master server and 2 worker agents with expose ports 80 (http) and 443 (https) for the load balancer within the k3d cluster

```bash
k3d cluster create dev-cluster -p "80:80@loadbalancer" -p "443:443@loadbalancer" --servers 1 --agents 2
```

### To run you local or custom image in k3d cluster

- Import the image into your cluster (e.g., `dev-cluster`)

```bash
k3d --cluster <cluster-name> image import <image-name>:<image-tag>
```

e.g.,

```bash
k3d --cluster dev-cluster image import <image-name>:<image-tag>

k3d -c dev-cluster image import <image-name>:<image-tag>
```

OR

```bash
k3d --cluster <cluster-name> images import <image-name-1>:<image-tag-1> <image-name-2>:<image-tag-2>
```

e.g.,

```bash
k3d --cluster dev-cluster images import <image-name-1>:<image-tag-1> <image-name-2>:<image-tag-2>

k3d -c dev-cluster images import <image-name-1>:<image-tag-1> <image-name-2>:<image-tag-2>
```

#### To test if the image is imported correclty in your cluster run the command

```bash
kubectl run <image-name> --image <image-name>:<image-tag>

k run <image-name> --image <image-name>:<image-tag>
```

- Now see if a pod with name the `<image-name>` is created

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

