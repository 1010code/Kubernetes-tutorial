
## Ingress
Ingress 能幫助我們將 Service 抽象化能夠自動的幫我們對應到相對的 IP 位置。簡單來說輸入某個 domain name 後 Ingress 能夠幫我們分配到相對應的 IP PORT 位置上。

### 部署兩個 Development
執行此指令會觸發 Replica Sets 然後產生相對應數量的 Pod

```bash
$ kubectl apply -f ingress.deployment.yaml 
``` 
### 部署兩個 Service

```bash
$ kubectl apply -f ingress.service.yaml
```

### 部署 Ingress
類似 Service 綁定 Pod，Ingress 透過 serviceName 指定需要綁定的 Service

```bash
$ kubectl apply -f ingress.yaml 
ingress "web" created

$ kubectl get ingress
NAME      HOSTS                           ADDRESS          PORTS     AGE
web       green.myweb.com,red.myweb.com   192.168.99.100   80        43s
```

這裡就會看到 green.myweb.com 與 red.myweb.com 都被綁定到 192.168.99.100 的位置
在雲端上必須要 `minikube addons enable ingress` 啟用 Ingress


Mac 輸入 `sudo vi /etc/hosts` 進入修改
``
192.168.99.100   green.myweb.com
192.168.99.100   red.myweb.com 
```
