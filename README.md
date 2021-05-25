# Cilium Installation

This repository contains Installation of Cilium using Minikube Cluster in Ubuntu. 

Prerequisites to install Cilium are :

```
Docker 
Kubernetes
Minikube >= v1.5.2 
```
To install the above prerequisites please use this [Installation guide](https://github.com/designanderror/Kubernetes-Minikube-Cheatsheet/blob/main/README.md#minikube-cheatsheet---kali-linux)

#### Install the Cilium CLI
Install the latest version of the Cilium CLI on your local machine. The Cilium CLI can be used to install Cilium, inspect the state of a Cilium installation, and enable/disable a variety of functionality.

```
curl -LO https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-amd64.tar.gz
sudo tar xzvfC cilium-linux-amd64.tar.gz /usr/local/bin
rm cilium-linux-amd64.tar.gz
```

#### Initialize a Minikube cluster with a CNI plugin

```
minikube start --network-plugin=cni
```

#### Install Cilium inside Minikube Cluster

```
cilium install
```

If the installation fails for some reason, run cilium status to retrieve the overall status of the Cilium deployment and inspect the logs of whatever pods are failing to be deployed.

The output should be similar to the following one:
```
   /¯¯\
/¯¯\__/¯¯\    Cilium:         OK
\__/¯¯\__/    Operator:       OK
/¯¯\__/¯¯\    Hubble:         disabled
\__/¯¯\__/    ClusterMesh:    disabled
   \__/

DaemonSet         cilium             Desired: 2, Ready: 2/2, Available: 2/2
Deployment        cilium-operator    Desired: 2, Ready: 2/2, Available: 2/2
Containers:       cilium-operator    Running: 2
                  cilium             Running: 2
Image versions    cilium             quay.io/cilium/cilium:v1.9.5: 2
                  cilium-operator    quay.io/cilium/operator-generic:v1.9.5: 2
                  
```

#### Deploy the connectivity test

```
cilium connectivity test
```

2 tests are expected to fail since Minikube is a single node cluster. Connectivity check pods for multi-node requires a cluster with more than one node.
