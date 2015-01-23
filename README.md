# Playground

A microservices playground built with docker and kubernetes.

## Prerequisites 

Requires Kubernetes

### Run Kubernetes locally with Vagrant

```
git clone https://github.com/GoogleCloudPlatform/kubernetes
cd kubernetes
export KUBERNETES_PROVIDER=vagrant
cluster/kube-up.sh
```

## Getting Started

Start dependencies

### Start Redis

```
cluster/kubectl.sh create -f github.com/myodc/playground/playground-redis.json
cluster/kubectl.sh create -f github.com/myodc/playground/playground-redis-service.json
```

### Start Registry

```
cluster/kubectl.sh create -f github.com/myodc/playground/playground-registry.json
cluster/kubectl.sh create -f github.com/myodc/playground/playground-registry-service.json
```

### Start Server

For more details about the server visit [github.com/myodc/playground-server](https://github.com/myodc/playground-server)

Set PLAYGROUND_KUBE_HOST, PLAYGROUND_KUBE_USER and PLAYGROUND_KUBE_PASS to the kubernetes master api in playground-server.json

```
cluster/kubectl.sh create -f playground-server.json
cluster/kubectl.sh create -f playground-server-service.json
```

### Start Web App

For more details about the web app visit [github.com/myodc/playground-web](https://github.com/myodc/playground-web)

Set API_BASE_URL in plaground-web.json to the playground server address

```
kubectl create -f playground-web.json
kubectl create -f playground-web-service.json
```

### Start Proxy

For more details about the proxy visit [github.com/myodc/playground-proxy](https://github.com/myodc/playground-proxy)

Set the PROXY_DOMAIN in playground-proxy.json 
Set the publicIPs field in playground-proxy-service.json to the ips of the minions on which the proxy will run

Start the proxy
```
kubectl create -f playground-proxy.json
kubectl create -f playground-proxy-service.json
```

Make sure DNS is setup correctly for your PROXY_DOMAIN and then visit http://playground-web.PROXY_DOMAIN
