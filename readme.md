# homeserver setup

this is the readme describing the whole setup of my homeserver

## server itself

the server itself is a `raspberry pi 4 model b` with 8G ram. connected to it is a 500G external ssd, from which the system also boots. it is connected via usb-3.

it is available in my home network under `homeserver.local`. i can just ssh into it on that url, given that i am on the system with the registered ssh key.

### kubernetes

installed on the server is a [k3s](https://k3s.io/) cluster. the cluster is bundled with traefik as its ingress. there are no specific configurations. obviously `kubectl`and `helm` are also installed.

```sh
curl -sfL https://get.k3s.io | sh -
# Check for Ready node, takes ~30 seconds
sudo k3s kubectl get node
```

## deployment

for the deployment i use [fluxcd](https://fluxcd.io/).

the bootstrapping command is as follows:
```sh
flux bootstrap github \
  --token-auth \
  --owner=only-a-technical-user \
  --repository=homeserver-cluster \
  --branch=main \
  --path=deploy \
  --personal
```

## components

### jenkins

url: `lab.steppler.ai/jenkins`

### authentik
