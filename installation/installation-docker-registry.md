# Setup CA for private registry 
​
## Rhel 7
#### Prerequisite
- Docker version 1.17.0
- Docker Compose
- Docker Repository component are on /Source 

### 1.) Prepare docker registry
user: root

```
cp -r /Source/tnprdregistry.tn.cloud.tar.gz /data/
cd /data
tar -xvzf tnprdregistry.tn.cloud.tar.gz
cd /data/tnprdregistry.tn.cloud
docker load -i nginx_1.12.1-alpine.tnv0.1.img
docker load -i registry.img
docker images
```

### 2.) Create docker certificate
user: root

```
vi /etc/pki/ca-trust/source/anchors/cloudop.crt

-----BEGIN CERTIFICATE-----
MIICojCCAYoCCQCaPl+gZIJVrTANBgkqhkiG9w0BAQsFADASMRAwDgYDVQQDDAdD
bG91ZE9QMCAXDTE4MDIxNDA2NTU0OFoYDzIxMTgwMTIxMDY1NTQ4WjASMRAwDgYD
VQQDDAdDbG91ZE9QMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsiDl
1srly/b4Rb3xPeuZZCGdlProK+mu2ym1uEnUjXZ5/cwSLbHjwu3A6IR6UfWtiIIY
uO+0S8tlDt5QRWLrUfo8zKyL8WmC+iH+mtSHugBUgjzZ0zTp7fok9YCIQpwd8QBT
Ery7zCmivTEYSzZHkZWya+t8nOj8FEhRlg3Ff428MGEsZhVdNDjLnwK93iLm0+9H
nARU041zzjRioc2/mWzUfqF6iZ/OM7qBYFEDXpNHQqM8et4lktj1h8udpZI0eY0w
JJKmlEJYwncdGfyb7LycjZ+xZIWJuX28S01UHYBPl/DzCeUhRz5ZfcNpW0QslYkd
UtLGa98CmwQZx4Mh3wIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQCq0FsV1+wO3uLq
UC5m78/fIKgK4o1VUFgUq4YgOEsovc+wMJjNFVKqYuXBK4nvZTptq1Cqyc/z4OgE
63wqYw46Rli8FCPsVo6mS0L9Xh2gZCiCDoTf/CsikWlp2LfdC9J9UZFWV+h7UWr+
cpgAaPB3OoUnTzwpSE14U8PR/iPAuBhJl8Efixrns1KN8Y8auIYlhMnhtu+N0Yoq
kHntv5cOs1QbGmsE6V1FbgF4WGAyILwgg5zWdjfi0Qwpt8wFPbOba9s61cT6GnVA
cr83gEDWMofXLQWj+r1xj3YSq2ubUbehBpnvCyrwiTM35/Nzb1CQoCjewXaWNDJY
Xn8HOrNG
-----END CERTIFICATE-----

cd /etc/pki/ca-trust/source/anchors
update-ca-trust extract
openssl verify cloudop.crt
```

### 3.) Run docker compose
user: root

```
systemctl restart docker
systemctl status docker
cd /data/tnprdregistry.tn.cloud
docker-compose -f docker-compose.yml up -d
docker ps
```

### 4.) Edit /etc/hosts
user: root

```
vi /etc/hosts

[ip address] tnprdregistry.tn.cloud
```

### 5.) Login docker repository
user: root

```
docker login https://tnprdregistry.tn.cloud:5443
username: xxxx 
password: xxxx
```
