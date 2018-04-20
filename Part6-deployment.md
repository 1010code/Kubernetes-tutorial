Replica Set 提供更彈性的selector，並不推薦開發者直接使用 kubectl create 等指令創建 Replica Set 物件，而是透過 Deployment 來創建新的 Replica Set。

Deployment 可以幫我們達成以下幾件事情：
- 部署一個應用服務(application)
- 協助 applications 升級到某個特定版本
- 服務升級過程中做到無停機服務遷移(zero downtime deployment)
- 可以Rollback到先前版本

## 攥寫 Deployment yaml

```bash
# deployment.yaml

---
apiVersion: apps/v1        # 使用 v1 版本的 api
kind: Deployment      # 類型為 Deployment
metadata:
  name: webserver         # Deployment 的名稱
spec:                 # 其他規格描述(Deployment)
  replicas: 3         # 運行三個 Pod (replicas: 3)
  selector:
    matchLabels:
      app: webserver
  template:           # 描述每個 Pod 規格
    metadata:
      labels: 
        app: webserver    # 標記名稱
    spec:             # 其他規格描述(Pod)
      containers:     # 描述容器內容
      - name: my-pod   # 將容器名稱
        image: andy6804tw/docker-nodejs-tutorial  # 使用 nginx 映像檔
        ports:
        - containerPort: 8080 # 指定使用 8080 port
```

- Deployment 
  - 物件內可以描述 Pod 的內容 (spec) 以及想要運行的個數 (ReplicaSet)。
- ReplicaSet
  - ReplicaSet 最主要的功能是在確保 Pod 指定的運行數量能達到所設定的數量。

## 部署 Deployment
```bash
$ kubectl apply -f deployment.yaml
```

## 查看 Replication Set
Deployment也會自動幫我們建立一個Replication Set來管理這些Pod

```bash
$ kubectl get rs
```

## 指令啟動 Service

```bash
$ kubectl expose deploy webserver --type=NodePort --name=demo-service
```

創建好之後，我們可以透過 minikube server 取得目前 demo 的網址，
```bash
$ minikube service demo-service --url
```


## 透過指令更新(rollout) webserver

```bash
$ kubectl set image deploy/webserver my-pod=andy6804tw/docker-nodejs-tutorial:Part1
```

查詢升級狀況
```bash
$ kubectl rollout status deploy/webserver
```

查看 rollout 歷史紀錄
```bash
$ kubectl rollout history deploy/webserver
```

rollout 到上一版
```bash
$ kubectl rollout undo deployment webserver
```

rollout 到某個特定版本
```bash
$ kubectl rollout undo deploy webserver --to-revision=3
```
