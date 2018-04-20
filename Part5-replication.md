# Replication Controller
Replica Sets 可以說是進化版的 Replication Controller，與 Replication Controller最大的差異在於，Replica Sets 提供了更彈性的selector。

此篇教你如何利用 Replication Controller 來擴展以及管理 Pod。

Replication Controller 就是 k8s 上用來管理 Pod 的數量以及狀態的 controller

在大多數情況下，我們不需要直接去操作 ReplicaSet，而是透過宣告 Deployment 物件。因為 Deployment 就已經包含了 ReplicaSet 的處理。

- Replication Controller 用 yaml 建立
- 在Replication Controller設定檔中可以指定同時有多少個相同的Pods運行在Kubernetes Cluster上
- 當某一Pod發生crash, failed，而終止運行時，Replication Controller會幫我們自動偵測，並且自動創建一個新的Pod，確保Pod運行的數量與設定檔的指定的數量相同


```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: my-replication-controller
spec:
  replicas: 3
  selector:
    app: webserver
  template:
    metadata:     
      labels:        # Pod 的標記
        app: webserver
    spec:                # 其他規格描述
      containers:        # 描述容器內容
      - name: docker-nodejs-tutorial   # 將容器名稱
        image: andy6804tw/docker-nodejs-tutorial     # 使用自己 Docker Hub 範例映像檔
        ports:
        - containerPort: 8080   # 指定使用 8080 port

```

## 部署 Replication 到 k8s 上

```bash
$ kubectl create -f replication.yaml    
```

## 部署 Service 到 k8s

```bash
kubectl apply -f service.yaml  
```

查詢目前服務:
```bash
$ kubectl get service 

NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP   10.96.0.1     <none>        443/TCP          2d
web          NodePort    10.107.3.80   <none>        8080:30059/TCP   3s
```

查詢ip:
```bash
$ minikube ip
```

