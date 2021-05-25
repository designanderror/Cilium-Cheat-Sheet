# Setting up Hubble Observability

Hubble is the observability layer of Cilium and can be used to obtain cluster-wide visibility into the network and security layer of your Kubernetes cluster.

#### Download the latest hubble release:
```
export HUBBLE_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/hubble/master/stable.txt)
curl -LO "https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-amd64.tar.gz"
curl -LO "https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-amd64.tar.gz.sha256sum"
sha256sum --check hubble-linux-amd64.tar.gz.sha256sum
tar zxf hubble-linux-amd64.tar.gz
sudo mv hubble /usr/local/bin
```

Run ```cilium status``` to validate that Hubble is enabled and running. The output should be like following:

```
    /¯¯\
 /¯¯\__/¯¯\    Cilium:         OK
 \__/¯¯\__/    Operator:       OK
 /¯¯\__/¯¯\    Hubble:         OK
 \__/¯¯\__/    ClusterMesh:    disabled
    \__/

DaemonSet         cilium                   Desired: 3, Ready: 3/3, Available: 3/3
Deployment        cilium-operator          Desired: 1, Ready: 1/1, Available: 1/1
Deployment        hubble-relay             Desired: 1, Ready: 1/1, Available: 1/1
Containers:       cilium                   Running: 3
                  cilium-operator          Running: 1
                  hubble-relay             Running: 1
Image versions    cilium-operator          quay.io/cilium/operator-generic:v1.9.5: 1
                  hubble-relay             quay.io/cilium/hubble-relay:v1.9.5: 1
                  cilium                   quay.io/cilium/cilium:v1.9.5: 3
```

#### Validate Hubble API Access

In order to access the Hubble API, create a port forward to the Hubble service from your local machine. This will allow you to connect the Hubble client to the local port 4245 and access the Hubble Relay service in your Kubernetes cluster.

```
cilium hubble port-forward&
```
Output will be like :
```
Forwarding from 0.0.0.0:4245 -> 4245
Forwarding from [::]:4245 -> 4245
```
#### Check Status of Hubble

```
hubble status
```

Output should be like :
```
Healthcheck (via localhost:4245): Ok
Current/Max Flows: 11917/12288 (96.98%)
Flows/s: 11.74
Connected Nodes: 3/3
```
