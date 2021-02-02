# Setup CA for private registry on MyMo Cloud
​
## UBUNTU
1. create cert
```bash
sudo mkdir -p /usr/local/share/ca-certificates/docker-cert
​
sudo vi /usr/local/share/ca-certificates/docker-cert/devdockerCA.crt
```
​
[insert cert content for registry you want to use]
​
```bash
sudo update-ca-certificates
sudo systemctl restart docker
```
​
## RHEL
1. create cert
```bash
vi /etc/pki/ca-trust/source/anchors/devdockerCA.crt
```
[insert cert content for registry you want to use ]
​
```bash
vi /etc/pki/ca-trust/source/anchors/cloudop.crt
```
[insert cert content cloudop]
​
```bash
update-ca-trust extract
openssl verify /etc/pki/ca-trust/source/anchors/devdockerCA.crt
systemctl restart docker.service
```
​
## Docker login
```bash
docker login nonprdregistry.myp.local:5443
Username : devadm
Password : D3vadm
```
​
## content cert
​
### nonprdregistry.myp.local:5443 cert
​
-----BEGIN CERTIFICATE-----
MIIDJDCCAgwCCQDzr8jKo8WROzANBgkqhkiG9w0BAQsFADASMRAwDgYDVQQDDAdD
bG91ZE9QMCAXDTE5MDgxNjAzNDEwMFoYDzIxMTkwNzIzMDM0MTAwWjCBkzELMAkG
A1UEBhMCVEgxEDAOBgNVBAgMB0Jhbmdrb2sxEDAOBgNVBAcMB0Jhbmdrb2sxIDAe
BgNVBAoMF1QuTi4gSU5DT1JQT1JBVElPTiBMVEQuMRswGQYDVQQLDBJTRSBDbG91
ZC1PcGVyYXRpb24xITAfBgNVBAMMGG5vbnByZHJlZ2lzdHJ5Lm15cC5sb2NhbDCC
ASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAL+o9AdfVYZieLMFSq82STIa
aHFRAhorDYgsSS/tm3ngsX/W9PqAfjLIy0cUcKpEPNlkcLKEC9B42TaxtEYweAkj
wSTr0MNkG+46VyIHrbdjrlsPUWbFENnWpmeOS9V7Www3BugtugmvwEFVHwbcxcYF
wMlXS8XzHqwID8KBGmD5dmEc60Cxxvz3WsOrJywIl2j0Ug6jzWZn5LbkI06o0dQI
xxDpa/ttOzT6mQqnDa5x1YjNDwbYKs0hmn31J0WDMfnQB4WcJtqek++pPk93XctP
YtMqiQe+eoQhZD/Dn3dXvjdLW874knLaEHQm5yqpsdN7UnOMVh4IjQNLkKFhpJEC
AwEAATANBgkqhkiG9w0BAQsFAAOCAQEABkPeq0MU8kskIuMKY8Ve4Pe+9mrckvjI
DXIgbiWifbDqOhPvT0wbsRG4Sqr59t6PGuvBR5K1D5hHgsdPNIwjChP2V5DTLXLK
N5NYgYTXLZXfoRtlaGQaO6Uc2vH/Rkxxs39VD5Ny59TqWooAArFzHdWRqRYW8Uts
ANdUKx3a+ziLONYrtzlcv9mQaMN19vLW1sXkL35kXbj6t+5gvrkdKCWaO70PbTH4
9yZMn6aoj7dYylsov0ijwQ9kh64CyZynxonEiZJ+ES0lfW9dqI0HzVX8OS8uyObX
S9FzFnWxehc+9HF3map1qoepwWTboEgDWIkE6NWKVPz5rQw0LENhwQ==
-----END CERTIFICATE-----
​
### mmdevpr.tnis.com:5443 cert
​
-----BEGIN CERTIFICATE-----
MIIDXTCCAkWgAwIBAgIJAL6QVUpzFjjlMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV
BAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5ldCBX
aWRnaXRzIFB0eSBMdGQwHhcNMTYxMjIzMDY1NDUxWhcNNDQwNTEwMDY1NDUxWjBF
MQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UECgwYSW50
ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB
CgKCAQEAusd3TTu/hAqAoQUvVpq0BJSH7Oe9osADoJB6cl4P1u8IE1mLbaMYL6vy
gkbVmYAfoH2ERXZSbgW4f1ziqynMZaBh6ObXl98LtQpTfVj1J9r8Gc4VDC5wfltf
3Tt6cXQLLyEvS6ckzFSNVv7S55gNEmVY/9vt2+CY/8biasNPyDY0LCtROtY4U+sV
/fo8LmOTpHvdJJ5/k5BCB6OtAJuWI6Y45xAggzfy586zz3jGlZzTTNqtLn1e9/x1
VXvNeiG+N95iMBOJXI0fF7iY3gkPmWF4pg74cSuMlm7xc/kFP8j4Nve/QcsAZ8ah
yyTWM/bVOS1RXCOOI5CBxoJa4kyJIQIDAQABo1AwTjAdBgNVHQ4EFgQUAaTIsxuc
WYEFYVKztoPeTs60aW0wHwYDVR0jBBgwFoAUAaTIsxucWYEFYVKztoPeTs60aW0w
DAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEAn8OBUVi1HI+tJlwS+7Fb
ct3u1RXN0D+pO+1Yx7hmGFzsdwK2ZEfZuqlArRXv3BPlm4YX9r0ayUCVtSAFZJM4
ZuzQuuWTBWhGNAaspiCrNRb36LHobtaHTiGyLx7ZA8058z88DDOSyGOpladvncPp
JJWHOYE3U7pRsqtdpphViW32yOOklWR0JiXOTkEvTE/gYetU7RwrzTx6K8KNE4SC
zK0dgUpZBPFZy/P80LNzenibWC03zjZnHQq1m887DRPoc1WS5TVb/d9QaSWirdP2
ZK28WiQvXpvAv+Da2+7I+z2A5HGHiUFooSxX5zDl1SP9VW6BXV1T4IIw8bTaBYJn
Ww==
-----END CERTIFICATE-----
​
### cloudop cert
​
vi /etc/pki/ca-trust/source/anchors/cloudop.crt
​
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
​
## Push images
​
```bash
vi /etc/hosts
```
add nonprdregistry.myp.local 
internal ip 172.31.227.5 for push image from local computer
external ip 10.82.19.235 for vm in cloud
​
```bash
docker tag mmdevpr.tnis.com:5443/tnindo/datahubconsumer:0.9 nonprdregistry.myp.local:5443/tnindo/datahubconsumer:0.9
docker push nonprdregistry.myp.local:5443/tnindo/datahubconsumer:0.9
```
​
## access vm
10.82.19.235
username : ubuntu
password : ubuntu
