# homeserver setup

this is the readme describing the whole setup of my homeserver

## server itself

the server itself is a `raspberry pi 4 model b` with 8G ram. connected to it is a 500G external ssd, from which the system also boots. it is connected via usb-3.

it is available in my home network under `homeserver.local`. i can just ssh into it on that url, given that i am on the system with the registered ssh key.

### certificates

to use tls i use a self signed certificate. i created the cert using the following commands:

```zsh
openssl genrsa -out myCA.key 2048
openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1024 -out myCA.pem -subj "/CN=HomeServerCA"

openssl genrsa -out homeserver.local.key 2048
openssl req -new -key homeserver.local.key -out homeserver.local.csr -subj "/CN=homeserver.local"

openssl x509 -req -in homeserver.local.csr -CA myCA.pem -CAkey myCA.key -CAcreateserial -out homeserver.local.crt -days 500 -sha256
```

## components

### jenkins

url: `homeserver.local/jenkins`

### harbor

**work in progress**

url: `homeserver.local/harbor`
