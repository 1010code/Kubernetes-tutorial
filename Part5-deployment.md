## 攥寫 Deployment yaml

```bash
# deployment.yaml
---
apiVersion: extensions/v1beta1        # 使用 v1 版本的 api
kind: Deployment      # 類型為 Deployment
metadata:
  name: nginx         # Deployment 的名稱
spec:                 # 其他規格描述(Deployment)
  replicas: 3         # 運行三個 Pod (replicas: 3)
  template:           # 描述每個 Pod 規格
    metadata:
      labels: 
        app: nginx    # 標記名稱
    spec:             # 其他規格描述(Pod)
      containers:     # 描述容器內容
      - name: nginx   # 將容器名稱
        image: nginx  # 使用 nginx 映像檔
        ports:
        - containerPort: 80 # 指定使用 80 port
```

- Deployment 
  - 物件內可以描述 Pod 的內容 (spec) 以及想要運行的個數 (ReplicaSet)。
- ReplicaSet
  - ReplicaSet 最主要的功能是在確保 Pod 指定的運行數量能達到所設定的數量。

## 部署 Deployment
```bash
$ kubectl apply -f deployment.yaml
```
